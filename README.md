Introduce
==========

The repository contains the rules for [krep] to import the source codes of
Netgear routers from its [NETGEAR-Open-Source-Code-for-Programmers-GPL] website.

Each router project was imported in different time. Because the rules are
updated accordingly with the late projects, the final importing stuffs will be
changed comparing with the actual files in the corresponding git repositories.
Generally, the last release with the updated rules will keep the precise
contents.

It's not hard to use `krep` with its subcommand `repo-import` to import Netgear
projects based on Broadcom router codes.

All official releases can be found at [NETGEAR-Open-Source-Code-for-Programmers-GPL].
Two file will be extracted from each of the release.

```bash
$ unzip R7000-V1.0.9.60_10.2.60_src.tar.zip
$ ls
R7000-V1.0.9.60_10.2.60_build_instructions.txt
R7000-V1.0.9.60_10.2.60_src.tar
```

`r7000.txt` assumed that each package should use its version as directory and
the build instruction need be in the directory. Following commands will handle
the directory and file.

```bash
$ tar xf R7000-V1.0.9.60_10.2.60_src.tar
$ mv R7000-V1.0.9.60_10.2.60_src R7000-V1.0.9.60_10.2.60
$ mv R7000-V1.0.9.60_10.2.60_build_instructions.txt R7000-V1.0.9.60_10.2.60
```

If there're several packages, the commands can be batched.

```bash
$ unzip *.zip
$ tar xf *.tar
$ ls *_src | while read f; do \
  mv $f ${f/_src/}; \
  mv ${f/_src/}*.txt ${f/_src/}; \
done
```

Once the releases are ready in the directories, `krep` can be used to import the
releases into git-repo projects in github.

```bash
$ krep repo-import --config-file r7000.xml R7000-* --pattern 'p:vendor_broadcom_router$'
```

The option `--pattern` would be used to control which project need to be
imported instead to import all project described in `manifest.xml`.

[krep]: http://github.com/cadappl/krep
[NETGEAR-Open-Source-Code-for-Programmers-GPL]: https://kb.netgear.com/2649/NETGEAR-Open-Source-Code-for-Programmers-GPL

