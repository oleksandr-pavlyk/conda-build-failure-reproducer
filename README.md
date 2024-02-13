# Reproducer for issue running conda-build

## Step to reproduce

```bash
conda build -c conda-forge --override-channels recipe/
```

## Observed output

```
(base) opavlyk@opavlyk-mobl:~/tmp/triage_conda-build$ conda build -c conda-forge --override-channels recipe/
WARNING: No numpy version specified in conda_build_config.yaml.  Falling back to default numpy value of 1.22
Adding in variants from internal_defaults
Attempting to finalize metadata for foo
Collecting package metadata (repodata.json): ...working... done
Solving environment: ...working... failed

# >>>>>>>>>>>>>>>>>>>>>> ERROR REPORT <<<<<<<<<<<<<<<<<<<<<<

    Traceback (most recent call last):
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda/exception_handler.py", line 17, in __call__
        return func(*args, **kwargs)
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda/cli/main.py", line 64, in main_subshell
        exit_code = do_call(args, parser)
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda/cli/conda_argparse.py", line 143, in do_call
        result = plugin_subcommand.action(getattr(args, "_args", args))
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda_build/plugin.py", line 10, in build
        execute(*args, **kwargs)
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda_build/cli/main_build.py", line 568, in execute
        outputs = api.build(
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda_build/api.py", line 253, in build
        return build_tree(
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda_build/build.py", line 3804, in build_tree
        packages_from_this = build(
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda_build/build.py", line 2474, in build
        output_metas = expand_outputs([(m, need_source_download, need_reparse_in_env)])
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda_build/render.py", line 923, in expand_outputs
        for output_dict, m in deepcopy(_m).get_output_metadata_set(
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda_build/metadata.py", line 2574, in get_output_metadata_set
        conda_packages = finalize_outputs_pass(
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda_build/metadata.py", line 934, in finalize_outputs_pass
        fm = finalize_metadata(
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda_build/render.py", line 637, in finalize_metadata
        build_unsat, host_unsat = add_upstream_pins(
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda_build/render.py", line 452, in add_upstream_pins
        build_deps, build_unsat, extra_run_specs_from_build = _read_upstream_pin_files(
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda_build/render.py", line 431, in _read_upstream_pin_files
        deps, actions, unsat = get_env_dependencies(
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda_build/render.py", line 151, in get_env_dependencies
        actions = environ.get_install_actions(
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda_build/environ.py", line 900, in get_install_actions
        actions = install_actions(prefix, index, specs, force=True)
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda/common/io.py", line 84, in decorated
        return f(*args, **kwds)
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda/plan.py", line 535, in install_actions
        txn = solver.solve_for_transaction(prune=prune, ignore_pinned=not pinned)
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda/core/solve.py", line 154, in solve_for_transaction
        unlink_precs, link_precs = self.solve_for_diff(
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda/core/solve.py", line 215, in solve_for_diff
        final_precs = self.solve_final_state(
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda/core/solve.py", line 380, in solve_final_state
        ssc = self._add_specs(ssc)
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda/core/solve.py", line 874, in _add_specs
        conflicts = ssc.r.get_conflicting_specs(
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda/resolve.py", line 1270, in get_conflicting_specs
        C = r2.gen_clauses()
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda/common/io.py", line 84, in decorated
        return f(*args, **kwds)
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda/resolve.py", line 1055, in gen_clauses
        for ms in self.ms_depends(prec):
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda/resolve.py", line 929, in ms_depends
        deps = [MatchSpec(d) for d in prec.combined_depends]
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda/models/records.py", line 366, in combined_depends
        result = {ms.name: ms for ms in MatchSpec.merge(self.depends)}
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda/models/match_spec.py", line 493, in merge
        reduce(lambda x, y: x._merge(y, union), group)
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda/models/match_spec.py", line 493, in <lambda>
        reduce(lambda x, y: x._merge(y, union), group)
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda/models/match_spec.py", line 525, in _merge
        final = this_component.merge(that_component)
      File "/home/opavlyk/miniconda3/lib/python3.9/site-packages/conda/models/match_spec.py", line 815, in merge
        raise ValueError(
    ValueError: Incompatible component merge:
      - '*mpich*'
      - 'mpi_mpich_*'

`$ /home/opavlyk/miniconda3/bin/conda build -c conda-forge --override-channels recipe/`

  environment variables:
    ACL_BOARD_VENDOR_PATH=/opt/Intel/OpenCLFPGA/oneAPI/Boards
                 CIO_TEST=<not set>
        CMAKE_PREFIX_PATH=/opt/intel/oneapi/compiler/2024.0:/opt/intel/oneapi/mkl/2024.0/lib/cma
                          ke:
    CONDA_ALLOW_SOFTLINKS=false
        CONDA_DEFAULT_ENV=base
                CONDA_EXE=/home/opavlyk/miniconda3/bin/conda
             CONDA_PREFIX=/home/opavlyk/miniconda3
    CONDA_PROMPT_MODIFIER=(base)
         CONDA_PYTHON_EXE=/home/opavlyk/miniconda3/bin/python
               CONDA_ROOT=/home/opavlyk/miniconda3
              CONDA_SHLVL=1
                    CPATH=/opt/intel/oneapi/compiler/2024.0/opt/oclfpga/include:/opt/intel/oneap
                          i/mkl/2024.0/include:
           CURL_CA_BUNDLE=<not set>
            DIAGUTIL_PATH=/opt/intel/oneapi/compiler/2024.0/etc/compiler/sys_check/sys_check.sh
                FTP_PROXY=<set>
              HTTPS_PROXY=<set>
               HTTP_PROXY=<set>
          LD_LIBRARY_PATH=/opt/intel/oneapi/compiler/2024.0/opt/oclfpga/host/linux64/lib:/opt/in
                          tel/oneapi/compiler/2024.0/opt/compiler/lib:/opt/intel/oneapi/compiler
                          /2024.0/lib:/opt/intel/oneapi/mkl/2024.0/lib:
               LD_PRELOAD=<not set>
             LIBRARY_PATH=/opt/intel/oneapi/compiler/2024.0/lib:/opt/intel/oneapi/mkl/2024.0/lib
                          /:
                  MANPATH=/opt/intel/oneapi/compiler/2024.0/documentation/en/man/common:
                  NLSPATH=/opt/intel/oneapi/compiler/2024.0/lib/locale/%l_%t/%N:/opt/intel/oneap
                          i/mkl/2024.0/share/locale/%l_%t/%N:
                 NO_PROXY=<set>
                     PATH=/home/opavlyk/miniconda3/bin:/opt/intel/oneapi/compiler/2024.0/opt/ocl
                          fpga/bin:/opt/intel/oneapi/compiler/2024.0/bin:/opt/intel/oneapi/mkl/2
                          024.0/bin:/home/opavlyk/miniconda3/condabin:/usr/local/sbin:/usr/local
                          /bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/usr/li
                          b/wsl/lib:/mnt/c/WINDOWS/system32:/mnt/c/WINDOWS:/mnt/c/WINDOWS/System
                          32/Wbem:/mnt/c/WINDOWS/System32/WindowsPowerShell/v1.0:/mnt/c/WINDOWS/
                          System32/OpenSSH:/mnt/c/Program Files/PuTTY:/mnt/c/Program Files/dotne
                          t:/mnt/c/Users/opavlyk/AppData/Local/Microsoft/WindowsApps:/mnt/c/User
                          s/opavlyk/AppData/Local/Programs/Microsoft VS Code/bin:/snap/bin
          PKG_CONFIG_PATH=/opt/intel/oneapi/compiler/2024.0/lib/pkgconfig:/opt/intel/oneapi/mkl/
                          2024.0/lib/pkgconfig:
       REQUESTS_CA_BUNDLE=<not set>
              SOCKS_PROXY=<set>
            SSL_CERT_FILE=<not set>
                ftp_proxy=<set>
               http_proxy=<set>
              https_proxy=<set>
                 no_proxy=<set>
              socks_proxy=<set>

     active environment : base
    active env location : /home/opavlyk/miniconda3
            shell level : 1
       user config file : /home/opavlyk/.condarc
 populated config files :
          conda version : 23.7.4
    conda-build version : 3.26.1
         python version : 3.9.12.final.0
       virtual packages : __archspec=1=x86_64
                          __glibc=2.31=0
                          __linux=5.15.133.1=0
                          __unix=0=0
       base environment : /home/opavlyk/miniconda3  (writable)
      conda av data dir : /home/opavlyk/miniconda3/etc/conda
  conda av metadata url : None
           channel URLs : https://repo.anaconda.com/pkgs/main/linux-64
                          https://repo.anaconda.com/pkgs/main/noarch
                          https://repo.anaconda.com/pkgs/r/linux-64
                          https://repo.anaconda.com/pkgs/r/noarch
          package cache : /home/opavlyk/miniconda3/pkgs
                          /home/opavlyk/.conda/pkgs
       envs directories : /home/opavlyk/miniconda3/envs
                          /home/opavlyk/.conda/envs
               platform : linux-64
             user-agent : conda/23.7.4 requests/2.31.0 CPython/3.9.12 Linux/5.15.133.1-microsoft-standard-WSL2 ubuntu/20.04.6 glibc/2.31
                UID:GID : 1000:1000
             netrc file : None
           offline mode : False


An unexpected error has occurred. Conda has prepared the above report.
If you suspect this error is being caused by a malfunctioning plugin,
consider using the --no-plugins option to turn off plugins.

Example: conda --no-plugins install <package>

Alternatively, you can set the CONDA_NO_PLUGINS environment variable on
the command line to run the command without plugins enabled.

Example: CONDA_NO_PLUGINS=true conda install <package>

If submitted, this report will be used by core maintainers to improve
future releases of conda.
Would you like conda to send this report to the core maintainers? [y/N]:
Timeout reached. No report sent.

```
