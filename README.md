# Autonomous-VPN-connect-tool
I created a very basic tool to connect Vpns automatically with bash scripting. In short, this tool is finding every file with .ovpn extension in a specific directory and present you to every choise. 
When you choose the ovpn file it is connecting automatically. 
That's all. 

#!/bin/bash

# Directory containing VPN files
ana_dizin="/home/kali"

# .ovpn uzantılı dosyaları bul ve listele
dosyalar=($(find "$ana_dizin" -type f -name "*.ovpn"))

# .ovpn dosyalarını teker teker listeleyerek numaralandır
echo "Please choose a VPN file:"
for ((i=0; i<${#dosyalar[@]}; i++)); do
  echo "$((i+1)). $(basename ${dosyalar[$i]})"
done

# Kullanıcıdan seçim yapmasını iste
read -p "VPN seçimi (1-${#dosyalar[@]}): " secim

# Check the entered VPN
if [[ $secim -ge 1 && $secim -le ${#dosyalar[@]} ]]; then
  secilen_dosya=${dosyalar[$((secim-1))]}
  echo "Seçilen VPN dosyası: $(basename $secilen_dosya)"
  
  # Connect to VPN file with OpenVPN
  sudo openvpn --config "$secilen_dosya"
else
  echo "Geçersiz seçim. Program sona eriyor."
fi

You can download it via git clone like this 
