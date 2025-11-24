# Doc Linux PC

## Installation
### Partitionnage
#### EndeavourOS
Swap file (no hibernation) + partition btrfs
### Installation de Arch en Dual Boot Windows 11 avec secure boot et Grub
1. Installer Windows 11
2. Désactiver le secure boot dans le bios
3. Installer sa distrib linux avec Grub (Si Snapshot, sinon systemd)
4. Sous linux, réinstaller grub pour pouvoir utiliser les CA Keys (clés de microsoft si j'ai bien compris) `grub-install --target=x86_64-efi --efi-directory=esp --bootloader-id=GRUB --modules="tpm" --disable-shim-lock`
    - remplacer `esp` par le chemin du boot, par exple /boot ou /boot/efi (pour EndeavourOS notamment)
6. Passer le secure boot en mode configuration "Setup Mode"
7. Installer sbctl `yay sbctl`
8. Configurer le secure boot : 
    - Checker l'état du secure boot `sbctl status`
    - Générer les clefs : `sbctl create-keys`
    - Ajouter les clefs + celles de Microsofts : `sbctl enroll-keys -m`
    - `sbctl status`
    - Vérifier la signature des clefs : `sbctl verify`
    - Si pas présent : `sbctl sign -s /boot/vmlinuz-linux`
    - Puis : `sbctl verify | sed -E 's|^.* (/.+) is not signed$|sbctl sign -s "\1"|e'`
    - Un dernier check avant le reboot : `sbctl`
    - Ajouter la signature auto lors des maj : `sbctl sign -s -o /usr/lib/systemd/boot/efi/systemd-bootx64.efi.signed /usr/lib/systemd/boot/efi/systemd-bootx64.efi`
9. Réactiver le secure boot dans le bios
10. Vérifier que tout fonctionne

### Installation Arch avec systemd-boot, secureboot, LUKS2 et TPM2
1. Passer le Secure Boot en Setup Mode
2. Installer ``

Chemin n'est pas /boot/loader mais /efi/loader sous Endeavour

## Config
### Pamac et ChaoticAUR
### Chezmoi

### Ordi avec GPU intégré et dédié (aka ordi portable)
 - Forcer le lancement d'une application sur le GPU dédié : `__NV_PRIME_RENDER_OFFLOAD=1 __GLX_VENDOR_LIBRARY_NAME=nvidia`
