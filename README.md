# gnome-session-ctl
![graph](https://user-images.githubusercontent.com/705123/94291012-4dc3b600-ff5b-11ea-8234-ef171d46f75c.png)

In GNOME 3.38.0 a gnome-session-ctl binary was added into gnome-session which gnome-settings-daemon needs creating a circular dependency relation.
This is resolved by moving it into its own package as the graph above represents.
