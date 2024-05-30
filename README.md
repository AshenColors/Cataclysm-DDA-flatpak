This is an attempt to make a proof-of-concept slash testing aid Flatpak repository for the 0.H-stable branch of CDDA. The repository builds using [Flatter](https://github.com/andyholmes/flatter) whenever the submodule reference updates, and dependabot updates it automatically on a (weekday, best-effort) daily basis. 

~~Note that the "version" column in `flatpak list` or `flatpak remote-ls` still appears as "0.F Frank", since this is sourced from AppStream metadata. I'm working on a fix that includes the build's version string, but just putting a new release tag in the appdata.xml didn't seem to work.~~ All appstream metadata issues have been fixed upstream.

Add the repository to your Flatpak installation with `flatpak remote-add CDDA-flatpak-dev https://ashencolors.github.io/Cataclysm-DDA-flatpak/index.flatpakrepo`, and install the build with `flatpak install org.cataclysmdda.CataclysmDDA//0.H`.

Alternatively, build the manifest locally with 
```
# (one-time) build setup
flatpak remote-add --user --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
flatpak install --user org.flatpak.Builder
# build
flatpak run org.flatpak.Builder --force-clean --sandbox --user --install --install-deps-from=flathub --ccache --repo=repo build-dir org.cataclysmdda.CataclysmDDA.json
# (optional) install debug package
flatpak install --user cataclysmdda-origin org.cataclysmdda.CataclysmDDA.Debug
```