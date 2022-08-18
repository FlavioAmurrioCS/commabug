
When there is a pyproject.toml(even an empty one) the following errors happens when there is a console_scripts with a comma in it
Having a pyproject.toml makes it so that enventually get_export_entry gets called from pip distlib whose's regex does not capture , under name capture group. If ,command only command gets capture, if only comma(,) there regex search returns None

Not having pyproject.toml seems to take a different path for which , actually is parse as a proper console_script
```python
Obtaining file:///Users/flavio/projects/comma_command_test
  Installing build dependencies: started
  Installing build dependencies: finished with status 'done'
  Checking if build backend supports build_editable: started
  Checking if build backend supports build_editable: finished with status 'done'
  Getting requirements to build editable: started
  Getting requirements to build editable: finished with status 'done'
  Preparing editable metadata (pyproject.toml): started
  Preparing editable metadata (pyproject.toml): finished with status 'done'
Building wheels for collected packages: comma
  Building editable for comma (pyproject.toml): started
  Building editable for comma (pyproject.toml): finished with status 'done'
  Created wheel for comma: filename=comma-1.0.0-0.editable-py2.py3-none-any.whl size=2683 sha256=710f921193f934858360ea92877465bf9aaf7a6d0b9a659817f7e6ee7c730a5a
  Stored in directory: /private/var/folders/pp/w77j3dpd557_rvb5v0pcf42c0000gn/T/pip-ephem-wheel-cache-8n9y0lwh/wheels/74/7b/69/8981b6a176bba8cee26d7af162bedae85ca04c8bdede17673f
Successfully built comma
Installing collected packages: comma
  Attempting uninstall: comma
    Found existing installation: comma 1.0.0
    Uninstalling comma-1.0.0:
      Successfully uninstalled comma-1.0.0
  Rolling back uninstall of comma
  Moving to /Users/flavio/projects/comma_command_test/venv/bin/,
   from /private/var/folders/pp/w77j3dpd557_rvb5v0pcf42c0000gn/T/pip-uninstall-eqxz0cnr/,
  Moving to /Users/flavio/projects/comma_command_test/venv/bin/comma
   from /private/var/folders/pp/w77j3dpd557_rvb5v0pcf42c0000gn/T/pip-uninstall-eqxz0cnr/comma
  Moving to /Users/flavio/projects/comma_command_test/venv/lib/python3.8/site-packages/__editable__.comma-1.0.0.pth
   from /private/var/folders/pp/w77j3dpd557_rvb5v0pcf42c0000gn/T/pip-uninstall-ac7hh33g/__editable__.comma-1.0.0.pth
  Moving to /Users/flavio/projects/comma_command_test/venv/lib/python3.8/site-packages/__editable___comma_1_0_0_finder.py
   from /private/var/folders/pp/w77j3dpd557_rvb5v0pcf42c0000gn/T/pip-uninstall-ac7hh33g/__editable___comma_1_0_0_finder.py
  Moving to /Users/flavio/projects/comma_command_test/venv/lib/python3.8/site-packages/comma-1.0.0.dist-info/
   from /Users/flavio/projects/comma_command_test/venv/lib/python3.8/site-packages/~omma-1.0.0.dist-info
ERROR: Exception:
Traceback (most recent call last):
  File "/Users/flavio/projects/comma_command_test/venv/lib/python3.8/site-packages/pip/_internal/cli/base_command.py", line 167, in exc_logging_wrapper
    status = run_func(*args)
  File "/Users/flavio/projects/comma_command_test/venv/lib/python3.8/site-packages/pip/_internal/cli/req_command.py", line 247, in wrapper
    return func(self, options, args)
  File "/Users/flavio/projects/comma_command_test/venv/lib/python3.8/site-packages/pip/_internal/commands/install.py", line 461, in run
    installed = install_given_reqs(
  File "/Users/flavio/projects/comma_command_test/venv/lib/python3.8/site-packages/pip/_internal/req/__init__.py", line 73, in install_given_reqs
    requirement.install(
  File "/Users/flavio/projects/comma_command_test/venv/lib/python3.8/site-packages/pip/_internal/req/req_install.py", line 790, in install
    install_wheel(
  File "/Users/flavio/projects/comma_command_test/venv/lib/python3.8/site-packages/pip/_internal/operations/install/wheel.py", line 727, in install_wheel
    _install_wheel(
  File "/Users/flavio/projects/comma_command_test/venv/lib/python3.8/site-packages/pip/_internal/operations/install/wheel.py", line 644, in _install_wheel
    generated_console_scripts = maker.make_multiple(scripts_to_generate)
  File "/Users/flavio/projects/comma_command_test/venv/lib/python3.8/site-packages/pip/_vendor/distlib/scripts.py", line 436, in make_multiple
    filenames.extend(self.make(specification, options))
  File "/Users/flavio/projects/comma_command_test/venv/lib/python3.8/site-packages/pip/_internal/operations/install/wheel.py", line 425, in make
    return super().make(specification, options)
  File "/Users/flavio/projects/comma_command_test/venv/lib/python3.8/site-packages/pip/_vendor/distlib/scripts.py", line 423, in make
    self._copy_script(specification, filenames)
  File "/Users/flavio/projects/comma_command_test/venv/lib/python3.8/site-packages/pip/_vendor/distlib/scripts.py", line 329, in _copy_script
    script = os.path.join(self.source_dir, convert_path(script))
  File "/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.8/lib/python3.8/posixpath.py", line 76, in join
    a = os.fspath(a)
TypeError: expected str, bytes or os.PathLike object, not NoneType

[notice] A new release of pip available: 22.2.1 -> 22.2.2
[notice] To update, run: pip install --upgrade pip

```