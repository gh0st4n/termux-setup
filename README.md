# T4n Termux Setup + Zig Version Selector

Script ini melakukan setup Termux lengkap dengan:

-   Paket dasar (curl, wget, git, neovim, unzip, bat, eza, tree, rxfetch)
-   Installer Zig dengan **menu pilihan versi & arsitektur**
-   Setup NVChad
-   Patching tema & font
-   Dan konfigurasi tambahan sesuai script

## 📦 Cara Menggunakan

Ada **2 metode**: 1) Clone repo 2) Copy--paste manual

# 1️⃣ Instalasi via Git Clone

``` sh
git clone https://github.com/<username>/<repo>.git](https://github.com/gh0st4n/termux-setup.git
cd termux-setup

chmod +x setup.sh
./setup.sh
```

# 2️⃣ Instalasi via Copy--Paste Manual

1.  Buka Termux, Lalu Ketik :

``` sh
nano setup.sh
```

2.  Copy Kode ini, kemudian **paste** ke nano.
``` sh
#!/data/data/com.termux/files/usr/bin/bash

# ===================================
# T4n Custom Termux Setup + Zig Menu
# ===================================

set -e

# === 0. AKSES STORAGE ===
termux-setup-storage

# === 1. UPDATE & UPGRADE ===
pkg update -y && pkg upgrade -y

# === 2. INSTALL PACKAGE DASAR ===
pkg install -y curl wget git neovim unzip bat eza tree rxfetch

# ============================================
#        ZIG DOWNLOAD LINK MAPPING
# ============================================

declare -A ZIG_LINKS=(
  # --- Versions with no binaries ---
  ["0.1.1_aarch64"]=""
  ["0.1.1_armv7a"]=""
  ["0.1.1_arm"]=""

  ["0.2.0_aarch64"]=""
  ["0.2.0_armv7a"]=""
  ["0.2.0_arm"]=""

  ["0.3.0_aarch64"]=""
  ["0.3.0_armv7a"]=""
  ["0.3.0_arm"]=""

  ["0.4.0_aarch64"]=""
  ["0.4.0_armv7a"]=""
  ["0.4.0_arm"]=""

  ["0.5.0_aarch64"]=""
  ["0.5.0_armv7a"]=""
  ["0.5.0_arm"]=""

  # --- 0.6.x ---
  ["0.6.0_aarch64"]="https://ziglang.org/download/0.6.0/zig-linux-aarch64-0.6.0.tar.xz"
  ["0.6.0_armv7a"]="https://ziglang.org/download/0.6.0/zig-linux-armv7a-0.6.0.tar.xz"

  # --- 0.7.x ---
  ["0.7.0_aarch64"]="https://ziglang.org/download/0.7.0/zig-linux-aarch64-0.7.0.tar.xz"
  ["0.7.0_armv7a"]="https://ziglang.org/download/0.7.0/zig-linux-armv7a-0.7.0.tar.xz"

  ["0.7.1_aarch64"]="https://ziglang.org/download/0.7.1/zig-linux-aarch64-0.7.1.tar.xz"
  ["0.7.1_armv7a"]="https://ziglang.org/download/0.7.1/zig-linux-armv7a-0.7.1.tar.xz"

  # --- 0.8.x ---
  ["0.8.0_aarch64"]="https://ziglang.org/download/0.8.0/zig-linux-aarch64-0.8.0.tar.xz"
  ["0.8.0_armv7a"]="https://ziglang.org/download/0.8.0/zig-linux-armv7a-0.8.0.tar.xz"

  ["0.8.1_aarch64"]="https://ziglang.org/download/0.8.1/zig-linux-aarch64-0.8.1.tar.xz"
  ["0.8.1_armv7a"]="https://ziglang.org/download/0.8.1/zig-linux-armv7a-0.8.1.tar.xz"

  # --- 0.9.x ---
  ["0.9.0_aarch64"]="https://ziglang.org/download/0.9.0/zig-linux-aarch64-0.9.0.tar.xz"
  ["0.9.0_armv7a"]="https://ziglang.org/download/0.9.0/zig-linux-armv7a-0.9.0.tar.xz"

  ["0.9.1_aarch64"]="https://ziglang.org/download/0.9.1/zig-linux-aarch64-0.9.1.tar.xz"
  ["0.9.1_armv7a"]="https://ziglang.org/download/0.9.1/zig-linux-armv7a-0.9.1.tar.xz"

  # --- 0.10.x ---
  ["0.10.0_aarch64"]="https://ziglang.org/download/0.10.0/zig-linux-aarch64-0.10.0.tar.xz"
  ["0.10.0_armv7a"]="https://ziglang.org/download/0.10.0/zig-linux-armv7a-0.10.0.tar.xz"

  ["0.10.1_aarch64"]="https://ziglang.org/download/0.10.1/zig-linux-aarch64-0.10.1.tar.xz"
  ["0.10.1_armv7a"]="https://ziglang.org/download/0.10.1/zig-linux-armv7a-0.10.1.tar.xz"

  # --- 0.11.x ---
  ["0.11.0_aarch64"]="https://ziglang.org/download/0.11.0/zig-linux-aarch64-0.11.0.tar.xz"
  ["0.11.0_armv7a"]="https://ziglang.org/download/0.11.0/zig-linux-armv7a-0.11.0.tar.xz"

  # --- 0.12.x ---
  ["0.12.0_aarch64"]="https://ziglang.org/download/0.12.0/zig-linux-aarch64-0.12.0.tar.xz"
  ["0.12.0_armv7a"]="https://ziglang.org/download/0.12.0/zig-linux-armv7a-0.12.0.tar.xz"

  ["0.12.1_aarch64"]="https://ziglang.org/download/0.12.1/zig-linux-aarch64-0.12.1.tar.xz"
  ["0.12.1_armv7a"]="https://ziglang.org/download/0.12.1/zig-linux-armv7a-0.12.1.tar.xz"

  # --- 0.13.0 ---
  ["0.13.0_aarch64"]="https://ziglang.org/download/0.13.0/zig-linux-aarch64-0.13.0.tar.xz"
  ["0.13.0_armv7a"]="https://ziglang.org/download/0.13.0/zig-linux-armv7a-0.13.0.tar.xz"

  # --- 0.14.x ---
  ["0.14.0_aarch64"]="https://ziglang.org/download/0.14.0/zig-linux-aarch64-0.14.0.tar.xz"
  ["0.14.0_armv7a"]="https://ziglang.org/download/0.14.0/zig-linux-armv7a-0.14.0.tar.xz"

  ["0.14.1_aarch64"]="https://ziglang.org/download/0.14.1/zig-linux-aarch64-0.14.1.tar.xz"
  ["0.14.1_armv7a"]="https://ziglang.org/download/0.14.1/zig-linux-armv7a-0.14.1.tar.xz"

  # --- 0.15.x ---
  ["0.15.1_aarch64"]="https://ziglang.org/download/0.15.1/zig-linux-aarch64-0.15.1.tar.xz"
  ["0.15.1_arm"]="https://ziglang.org/download/0.15.1/zig-arm-linux-0.15.1.tar.xz"

  ["0.15.2_aarch64"]="https://ziglang.org/download/0.15.2/zig-linux-aarch64-0.15.2.tar.xz"
  ["0.15.2_arm"]="https://ziglang.org/download/0.15.2/zig-arm-linux-0.15.2.tar.xz"
)

# ============================================
#            MENU VERSI ZIG
# ============================================

VERSIONS=(
  0.1.1 0.2.0 0.3.0 0.4.0 0.5.0
  0.6.0 0.7.0 0.7.1
  0.8.0 0.8.1
  0.9.0 0.9.1
  0.10.0 0.10.1
  0.11.0
  0.12.0 0.12.1
  0.13.0
  0.14.0 0.14.1
  0.15.1 0.15.2
)

echo "===== PILIH VERSI ZIG ====="
i=1
for v in "${VERSIONS[@]}"; do
  echo "$i) $v"
  ((i++))
done

read -p "Pilih angka versi: " VSEL
VERSION="${VERSIONS[VSEL-1]}"

# ============================================
#            MENU ARSITEKTUR
# ============================================

ARCHS=(aarch64 armv7a arm)

echo
echo "===== PILIH ARSITEKTUR ====="
echo "1) aarch64 (64-bit)"
echo "2) armv7a (32-bit)"
echo "3) arm (32-bit = 0.15.1 & 0.15.2)"

read -p "Pilih angka arsitektur: " ASEL
ARCH="${ARCHS[ASEL-1]}"

KEY="${VERSION}_${ARCH}"
URL="${ZIG_LINKS[$KEY]}"

if [[ -z "$URL" ]]; then
  echo "[ERROR] Zig versi $VERSION untuk arsitektur $ARCH tidak tersedia!"
  exit 1
fi

echo "[*] Download Zig $VERSION ($ARCH)..."
wget "$URL" -O zig.tar.xz

mkdir -p ~/.lang
rm -rf ~/.lang/zig
tar -xf zig.tar.xz -C ~/.lang
mv ~/.lang/zig-* ~/.lang/zig

echo 'export PATH="$HOME/.lang/zig:$PATH"' >> ~/.bashrc

# ====================
#    INSTALL NVCHAD
# ====================

echo "[*] Install NVChad..."
rm -rf $HOME/.config/nvim
git clone https://github.com/NvChad/starter $HOME/.config/nvim
cd ~/.config/nvim
rm -rf .git

# ===========
#    Other
# ===========

# === INSTALL FONT FIRA CODE NERD ===
echo "[*] Mengunduh FiraCode Nerd Font..."
wget https://github.com/ryanoasis/nerd-fonts/releases/download/v3.4.0/FiraCode.zip -O FiraCode.zip
unzip -o FiraCode.zip -d FiraCode
rm FiraCode.zip

mkdir -p $HOME/.termux/fonts
mv FiraCode/FiraCodeNerdFontMono-Regular.ttf font.ttf
mv font.ttf $HOME/.termux/
rm -rf FiraCode

echo "[*] Menyiapkan .bashrc..."

cat > $HOME/.bashrc << 'EOF'
# === TERMUX CUSTOM CONFIG ===
clear
rxfetch

# PATH Zig
export PATH="$HOME/.lang/zig:$PATH"

# EDITOR default
export EDITOR="nvim"

# === ALIAS KHUSUS ===
alias cat='bat --theme=base16'
alias ls='eza --icons=always --color=always'
alias la='eza --icons=always --color=always -a'
alias ll='eza --icons=always --color=always -la'
alias tree='eza --icons=always --tree'
alias grep='grep --color=auto'
alias update='pkg update -y && pkg upgrade -y'

# === PROMPT CUSTOM ===
PS1='\n\[\e[1;31m\]┌──>\[\e[0m\] [ \u @ \h ] <<|= User =|>> [ \d ] [ \W ] \n\[\e[1;31m\]└{₿}->>\[\e[0m\] '
EOF

# Reload .bashrc
source $HOME/.bashrc

echo "[*] Menyiapkan Themes..."

cat > $HOME/.termux/colors.properties << 'EOF'
foreground:   #bfc9db
background:   #0f0f17

color0:       #13141c
color8:       #646a73

color1:       #d78787
color9:       #d78787

color2:       #afbea2
color10:      #afbea2

color3:       #e4c9af
color11:      #e4c9af

color4:       #a1bdce
color12:      #a1bdce

color5:       #d7beda
color13:      #d7beda

color6:       #b1e7dd
color14:      #b1e7dd

color7:       #bfc9db
color15:      #858893
EOF

# ============
#    FINISH
# ============

echo -e "\n==============================="
echo "[*] SETUP SELESAI!"
echo "Restart Termux."
echo "Zig versi $VERSION ($ARCH) terinstall."
echo "Path: ~/.lang/zig"
echo "==============================="

read -p "Apakah ingin restart Termux? [Y/n]: " confirm
confirm=${confirm:-Y}

if [[ "$confirm" =~ ^[Yy]$ ]]; then
    echo "Merestart Termux..."
    exec termux-reload-settings
    exit 0
else
    echo "Lewati restart. Silakan restart Termux manual jika diperlukan. Jalankan . .bashrc"
fi
```

3.  Simpan file:

```
    CTRL + X
    Y
    ENTER
```


4.  Jalankan:

``` sh
chmod +x setup.sh
./setup.sh
```

## 💡 Catatan

-   Script sudah otomatis mengunduh Zig sesuai versi & arsitektur
    pilihan.
-   Instalasi NVChad dan konfigurasi tambahan dilakukan otomatis.
-   Setelah instalasi selesai, **restart Termux** supaya PATH dan font
    aktif.
