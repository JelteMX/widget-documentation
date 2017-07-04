# Troubleshooting `Check widgets`

**This is copied from an answer I gave on the forum**

I had a problem recently where widgets woudn't build and the log only showed "dojo:dist" failed. So I did a bit of a dirty hack to make sure I get a better output. These are the steps (I did this for MX 6.5.0, but it's applicable in every version) :

Open Notepad as an Administrator. So find Notepad in your Startmenu, Right click -> Open as Administrator

Open Gruntfile.js (using Notepad) that is located at *C:\Program Files\Mendix\6.5.0\modeler\tools\grunt\*

At line nr 9 you see:

grunt.loadNpmTasks('grunt-dojo');

Add the following line after this (so on line nr 10):

grunt.option('verbose', true);

Save the file and close Notepad

Go back to Modeler, run Tools --> Check widgets, check the logfile again

The bundle log you mentioned should contain verbose output now, and this might help you debug the issue.

Why this hack? Gruntfile.js is used by Grunt, which is used in the Modeler to create a dojo build. So these tasks are designed to bundle widgetfiles. By using the Check widgets tool in the Modeler, it tries to bundle everything. Normally Grunt will only do minimal output. By adding the verbose option it will give you more output, which helps you pinpoint issues with bundling widgets.
