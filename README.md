# Qubes SaltStack configuration of Videos Playback VM

This is just a placeholder to Codeberg where this project source code lives: ( https://codeberg.org/brunoschroeder/qubes-salt-video-playback )

---
Reading our forum, I came across this great contribution from Bearillo, balko and qubist (with NeuroNX and tempmail):

( https://forum.qubes-os.org/t/improve-video-playback-performance-including-youtube-ytfzf/21946 )

The folks present us with a machine with some tools that enhance video playback from youtube, rumble and other online platforms, as well as offline video:

- mpv
- fzf
- smplayer
- vlc

### Sometimes people just need a short example (my wishful thinking)
For obvious reasons, I only use SaltStack to create and configure my VMs, but unfortunately in our great forum, a lot of setp-by-step configs do not come with the SaltStack configuration. I guess it's because of the learning curve, therefore I decided to contribute with my Salt files and a detailed step-by-step that could help people struggling on the learning curve. Reading the very short `sls` files and the `top` files and the documentation (and forum) could bring some people to the "A-ha!" moment and realisation of how Salt works. All feedback is welcome, please use the issues on this codeberg page.

Starting point for SaltStack on Qubes:

( https://www.qubes-os.org/doc/salt/ )


## Installation

On some VM:

1. Clone this repo (remember the $PATH).

```
git clone https://codeberg.org/brunoschroeder/qubes-salt-video-playback
```

On dom0:

1. Bring the repo in:

```
sudo qvm-run --pass $VM "cd ${PATH} && git bundle create - --all" > /tmp/qubes-salt-video-playback.pack
DOM0PATH=<chose your path>
cd $DOM0PATH
git clone /tmp/qubes-salt-video-playback.pack

```

2. Set the environment. Let's use the user-dirs at `/srv/user_salt/`:

```
sudo qubesctl top.enable qubes.user-dirs
sudo qubesctl state.highstate

sudo ln -sv $DOM0PATH/qubes-salt-video-playback/nav  /srv/user_salt/

```
3. Have the Template ready:

```
sudo qubesctl top enable nav.nav-tmpl
sudo qubesctl --show-output state.highstate
sudo qubesctl --show-output --skip-dom0 --targets=template-nav-videos state.apply

```

4. Now, make the VM:

```
sudo qubesctl top enable nav.nav
sudo qubesctl --show-output state.highstate
sudo qubesctl --show-output --skip-dom0 --targets=nav-videos state.apply

```

5. Now enjoy, all the apps are accessible via the menu under **nav-videos**.




