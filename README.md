# This is an attempt to better improve the process of using krun. Do NOT use/build this fork...use teohhanhui/krun (one of their branches) or slp/krun!



<h3>~Info about krun...<br><br></h3>
<h1>`Slp and Teohhanhui are the main people working on krun. Please buy Teohhanhui a coffee (link in their guide)</h1>

`krun` allows you to run arbitrary programs from your system in a microVM. It's comprised of two small programs:

- `krun`: links against [libkrun](https://github.com/containers/libkrun) to create the microVM.

- `krun-guest`: acts as an entrypoint inside the microVM to set up the environment for running your program.

## Using

``` sh

Usage: krun [OPTIONS] COMMAND [COMMAND_ARGS...]
OPTIONS:
        -h    --help                Show help
              --net=NET_MODE        Set network mode
              --passt-socket=PATH   Instead of starting passt, connect to passt socket at PATHNET_MODE can be either TSI (default) or PASST

COMMAND:      the command you want to execute in the vm
COMMAND_ARGS: arguments of COMMAND

```

## Running graphical applications

If [sommelier](https://chromium.googlesource.com/chromiumos/platform2/+/master/vm_tools/sommelier) is installed in your system, `krun` will use it to connect to the Wayland session on the hosts, allowing you to run graphical applications in the microVM.

GPU acceleration is also enabled on systems supporting [DRM native context](https://indico.freedesktop.org/event/2/contributions/53/attachments/76/121/XDC2022_%20virtgpu%20drm%20native%20context.pdf) (freedreno, amdgpu, asahi).

## Running x86/x86_64 on aarch64

If [FEX-Emu](https://fex-emu.com/) is installed in your system, `krun` will configure `binfmt_misc` inside the microVM so x86/x86_64 programs can be run transparently on it.

## Motivation

This tool is mainly intended to enable users to easily run programs designed for 4K-page systems on systems with a different page size, with [Asahi Linux](https://asahilinux.org/) being the prime example of this use case.

Other potential use cases could be software isolation, accessing privileged kernel features (provided by the guest) or local testing.`

The aim of this fork is to make this stuff simpler for the non-nerdy end-user to understand and, provided they understand the risks of running unreleased software (like NOT asking the Asahi folk for support about it...), get krun up and running.

Don't expect any of this to work. I would *not* clone this repository and attempt to use it on your system. Note: I won't be using the distrobox (this could break your system- do not do!)
