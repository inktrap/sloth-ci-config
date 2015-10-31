*****************
 ROADMAP
*****************

This is my personal roadmap for sloth-ci

- DONE: run sloth behind nginx
- DONE: testing via dummy-provider
- TODO: gogs validator
- TODO: python 3.2 compatibility

*****************
 BUGS?
*****************

I don't really know which of them are bugs, because the documentation is a little bit sparse. I wrote this stuff down directly, so some points may sound a little bit harsh, but that should not be the case. Let's start what 

- general question: is it okay to use relative paths or paths like ``~/foo/bar``?
- the work_dir in ``app.yml`` is confusing: this is relative to which dir?
  - the dir where sloth-ci is called,
  - where app.yml is
  - or where sloth.yml is?
  - can I configure this? If so, where?
- i did not install sloth-ci.ext.file_logs, but my app config was like this and sloth-ci did not complain.

    extensions:
        error_logs:
            module: logs
            path: ~/sloth/test
            filename: test-errors.log
            level: ERROR
        debug_logs:
            module: logs
            path: ~/sloth/test
            filename: test-debug.log
            level: DEBUG

*****************
* ACTIONS
*****************


- all actions are happening relative to the work_dir! This is not documented, right?
- all actions are executed via subprocess.
   - That should be documented somewhere
   - Also, this is highly insecure, I could overwrite everything where I have permission to write.
   - This is not bound to the output directory at all!
   - Also: shell=true is highly insecure!

Basically actions are shell-scripts that I can run as the user that runs sloth-ci.


*****************
* LOGGING
*****************

 - it appears that sloth-ci does not honor the logdir setting in sloth.yml. What should this setting express?
    - One logdir for all apps?
    - And an app only determines the log-filename?

 - the ``access_log`` is more like a http-log, like apaches access_log, right?

 - ``error_log`` is more like a backend log, there is a lot of stuff that went fine

 - I do not get an error output/log if a dir is not there or the action was not successful
 - I do not get a confirmation that an action was successful (like, when logging is on debug-level)

 - if I have test/incoming and it produces output, how do i create the default
   view for test/ with the created results? sloth-ci checks if there is a listener
   configured and if not 404s and as I see, there is no way to access the
   output of actions via sloth.

 - currently sloth is nice, but it is more like a post-recieve hook, not like
   a ci-server that is capable of showing results.

