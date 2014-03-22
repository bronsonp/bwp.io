---
layout: post
title: "A workaround for a six year old Matlab bug"
description: ""
tags: [matlab]
---

For a long time I have been frustrated by a Matlab graphics bug that is specific to dual screens on Linux. When exporting plots or opening the plot editor, Matlab sometimes crashes with the error:

{% highlight matlab %}
java.lang.IllegalArgumentException: adding a container to a container on a different GraphicsDevice
at java.awt.Component.checkGD(Unknown Source)
at java.awt.Container.addImpl(Unknown Source)
at java.awt.Container.add(Unknown Source)
at com.mathworks.hg.peer.FigurePanel.doAdd(FigurePanel.java:215)
at com.mathworks.hg.peer.FigurePanel.assembleFigurePanel(FigurePanel.java:203)
at com.mathworks.hg.peer.FigurePanel.reconstructFigurePanel(FigurePanel.java:131)
at com.mathworks.hg.peer.FigurePanel.handleNotification(FigurePanel.java:88)
... [trimmed]
{% endhighlight %}

The error occurs when the figure is not on the primary monitor. When this bug triggers, it destroys the figure that you were working on. It was reported to Mathworks back in 2008 ([forum thread](http://www.mathworks.com.au/matlabcentral/newsreader/view_thread/169024), [bug report](http://www.mathworks.com/support/bugreports/383414)). It's very frustrating that they have left this unfixed for so long.

In my code, I implement a workaround that moves the figure to the primary monitor. This runs before the plot is exported, so that my scripts don't run into this problem if the window manager just happens to place the figure window on the wrong screen.

This is the code:
{% highlight matlab %}
figh = ...; % the handle of the newly created figure

if isunix()
    set(figh, 'Units', 'pixels');
    posn = get(figh, 'Position');

    % This attempts to work around the Matlab bug where an exception is
    % throw when exporting graphics if the figure window is not on the
    % primary monitor. The exception is:
    %
    % java.lang.IllegalArgumentException: adding a container to a container on a different GraphicsDevice
    %   at java.awt.Component.checkGD(Unknown Source)
    % 	at java.awt.Container.addImpl(Unknown Source)
    % 	at java.awt.Container.add(Unknown Source)
    % 	at com.mathworks.hg.peer.FigurePanel.doAdd(FigurePanel.java:215)
    % 	at com.mathworks.hg.peer.FigurePanel.assembleFigurePanel(FigurePanel.java:203)
    % 	at com.mathworks.hg.peer.FigurePanel.reconstructFigurePanel(FigurePanel.java:131)
    % 	at com.mathworks.hg.peer.FigurePanel.handleNotification(FigurePanel.java:88)
    %   ... [trimmed]
    %
    % The workaround is to identify the "primary monitor" according to
    % Java AWT, and then place the figure on that monitor.

    % Find the primary monitor
    screens = java.awt.GraphicsEnvironment.getLocalGraphicsEnvironment().getScreenDevices();
    primary = screens(1); % assume primary monitor is first in the array
    bounds = primary.getDefaultConfiguration().getBounds();

    % bounds is a java.awt.Rectangle object
    x = bounds.x;
    y = bounds.y;
    width = bounds.width;
    height = bounds.height;

    % Center the figure on this same window
    posn(1:2) = [(x + width/2 - posn(3)/2), (y + height/2 - posn(4)/2)];
    set(figh, 'Position', posn);
end
{% endhighlight %}

It uses Java to detect the primary monitor and move the figure there. This same bug also triggers when opening the property editor (Tools -> Edit Plot, then double clicking on the axes) but this code cannot help there because the property editor creates a new window and its placement is up to your window manager. The only workaround in that case is to configure your window manager to always place the property editor window on your primary monitor.
