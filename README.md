# T4n Termux Setup + Zig Version Selector

Script ini melakukan setup Termux lengkap dengan:

-   Paket dasar (curl, wget, git, neovim, unzip, bat, eza, tree, rxfetch)
-   Install Zig 0.15.2
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

# === 0. AKSES STORAGE ===
termux-setup-storage

# === 1. UPDATE SISTEM ===
pkg update -y && pkg upgrade -y

# === 2. INSTALL PACKAGE UTAMA ===
pkg install -y curl wget git neovim unzip bat eza tree rxfetch

# === 3. DETEKSI ARSITEKTUR ===
ARCH_RAW=$(uname -m)

if [[ "$ARCH_RAW" == "aarch64" ]]; then
    ARCH="aarch64"
    ZIG_URL="https://ziglang.org/download/0.15.2/zig-aarch64-linux-0.15.2.tar.xz"
elif [[ "$ARCH_RAW" == "armv7l" || "$ARCH_RAW" == "armv8l" ]]; then
    ARCH="arm"
    ZIG_URL="https://ziglang.org/download/0.15.2/zig-arm-linux-0.15.2.tar.xz"
else
    echo "Arsitektur tidak dikenali: $ARCH_RAW"
    exit 1
fi

echo "[*] Arsitektur terdeteksi: $ARCH"
echo "[*] Download Zig dari: $ZIG_URL"

# === 4. INSTALL ZIG ===
wget "$ZIG_URL" -O zig.tar.xz
mkdir -p $HOME/.lang
tar -xf zig.tar.xz
rm zig.tar.xz

# cari folder zig hasil extract (pattern aman)
ZIG_FOLDER=$(find . -maxdepth 1 -type d -name "zig-*" | head -1)
mv "$ZIG_FOLDER" "$HOME/.lang/zig"

# === 5. INSTALL FONTS ===
echo "[*] Download font FiraCode Nerd Font..."
wget https://github.com/ryanoasis/nerd-fonts/releases/download/v3.4.0/FiraCode.zip -O FiraCode.zip
unzip -o FiraCode.zip -d FiraCode
rm FiraCode.zip

# rename → font.ttf
mv FiraCode/FiraCodeNerdFontMono-Regular.ttf font.ttf
mkdir -p $HOME/.termux
mv font.ttf $HOME/.termux/

rm -rf FiraCode

# === 6. BUAT THEME TERMINAL (color.properties) ===
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

# === 7. BUAT .bashrc BARU ===
cat > $HOME/.bashrc << 'EOF'
# === TERMUX CUSTOM CONFIG ===
clear
rxfetch

# PATH Zig
export PATH="$HOME/.lang/zig:$PATH"

# Default editor
export EDITOR="nvim"

# ALIAS
alias cat='bat --theme=base16'
alias ls='eza --icons=always --color=always'
alias la='eza --icons=always --color=always -a'
alias ll='eza --icons=always --color=always -la'
alias tree='eza --icons=always --tree'
alias grep='grep --color=auto'
alias update='pkg update -y && pkg upgrade -y'

# Prompt
PS1='\n\[\e[1;31m\]┌──>\[\e[0m\] [ \u @ \h ] <<|= User =|>> [ \d ] [ \W ] \n\[\e[1;31m\]└{₿}->>\[\e[0m\] '
EOF

source $HOME/.bashrc

# === 8. INSTALL NVCHAD ===
rm -rf $HOME/.config/nvim
git clone https://github.com/NvChad/starter $HOME/.config/nvim

echo -e "\n==================================="
echo "[*] SETUP LENGKAP!"
echo "- Arsitektur: $ARCH"
echo "- Zig terinstall di ~/.lang/zig"
echo "- Font aktif: ~/.termux/font.ttf"
echo "- Theme aktif: ~/.termux/color.properties"
echo "Restart Termux untuk menerapkan font + theme."
echo "Restar : . .bashrc"
echo "Lalu Jalankan perintah nvim"
echo "==================================="

read -p "Apakah ingin restart Termux? [Y/n]: " RESP
RESP=${RESP:-Y}

if [[ "$RESP" == "Y" || "$RESP" == "y" ]]; then
    echo "[*] Restarting Termux..."
    termux-reload-settings
    echo "[*] Keluar/Exit untuk MeReload Semua..."
else
    echo "[*] Tidak restart. Restart manual jika tampilan belum berubah."
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
