.PHONY: install
install:
	@cd PKGBUILDs/${package} && makepkg -scif --noconfirm

.ONESHELL:
aur:
	@mkdir -p .aur && cd .aur
	@git clone "https://aur.archlinux.org/${package}.git"
	@cd ${package}
	@echo "==================================== Viewing ${package}"
	@cat PKGBUILD
	@echo "===================================="
	@echo -n "Press enter to continue, or Ctrl+C to quit. " && read
	@makepkg -sc
	@sudo pacman -U *.pkg.tar.xz

.PHONY: refresh-keys
refresh-keys:
	@sudo pacman-key --populate
	@sudo pacman-key --refresh-keys

# https://old.reddit.com/r/archlinux/comments/5r5ep8
# 1. Disable bitmap fonts (not scalable for modern HiDPI displays)
# 2. Enable sub-pixel RGB rendering
# 3. Enable the LCD filter (reduces color fringing)
.PHONY: fontconfig
fontconfig:
	@sudo ln -sf /etc/fonts/conf.avail/70-no-bitmaps.conf /etc/fonts/conf.d
	@sudo ln -sf /etc/fonts/conf.avail/10-sub-pixel-rgb.conf /etc/fonts/conf.d
	@sudo ln -sf /etc/fonts/conf.avail/11-lcdfilter-default.conf /etc/fonts/conf.d

# 1. Always use emoji (best with the kitty terminal emulator)
# 2. Install global packages to /usr/local
.PHONY: yarnconfig
yarnconfig:
	@yarn config set -- --emoji true
	@yarn config set prefix /usr/local

.PHONY: rust
rust:
	@rustup install stable
	@rustup default stable

.PHONY: gnome
gnome:
	@../gnome/.config/gnome/extensions.sh
	@../gnome/.config/gnome/antialiasing.sh
	@../gnome/.config/gnome/arc-dark-gtk-theme.sh
	@../gnome/.config/gnome/breeze-cursor-theme.sh

.PHONY: clean
clean:
	@rm -fv PKGBUILDs/**/*.pkg.tar.xz
	@rm -fv PKGBUILDs/**/*.xpi
	@rm -fv PKGBUILDs/**/*.tar.gz
	@rm -fv PKGBUILDs/**/*.tar.bz2
	@rm -fv PKGBUILDs/**/*.vim
	@rm -rfv .aur
