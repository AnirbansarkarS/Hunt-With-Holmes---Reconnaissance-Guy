# 🔍 Hunt with Holmes

<div align="center">

![Version](https://img.shields.io/badge/version-2.0-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Bash](https://img.shields.io/badge/bash-5.0%2B-brightgreen.svg)
![Platforms](https://img.shields.io/badge/platforms-80%2B-orange.svg)

**A powerful OSINT tool to track usernames across 80+ social media platforms**

[Features](#features) • [Installation](#installation) • [Usage](#usage) • [Platforms](#platforms-covered) • [Contributing](#contributing)

</div>

---

## 📋 Table of Contents

- [About](#about)
- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Platforms Covered](#platforms-covered)
- [Output](#output)
- [Examples](#examples)
- [Legal Disclaimer](#legal-disclaimer)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

---

## 🎯 About

**Hunt with Holmes** is a comprehensive OSINT (Open Source Intelligence) tool designed for security researchers, investigators, and penetration testers. It automates the process of searching for a specific username across 80+ social media platforms and websites, helping you build a digital footprint profile quickly and efficiently.

---

## ✨ Features

- 🚀 **Fast & Efficient** - Quickly scans 80+ platforms in minutes
- 💾 **Auto-Save Results** - Automatically saves found profiles to a text file
- 🎨 **Colorful Interface** - Easy-to-read color-coded output
- 🔍 **Comprehensive Coverage** - Checks major and niche social platforms
- 🛡️ **Info-Stealer Database Check** - Checks if credentials were compromised
- 📊 **Clean Output** - Organized results with clear found/not found status
- 🔄 **Interrupt Handling** - Gracefully handles Ctrl+C interruptions
- 📝 **Text Export** - All found URLs saved to `[username].txt`

---

## 🔧 Prerequisites

Before running Hunt with Holmes, ensure you have the following installed:

- **Bash** (version 5.0 or higher)
- **curl** - For making HTTP requests
- **jq** - For parsing JSON responses
- **grep** - For pattern matching

### Install Dependencies

**On Debian/Ubuntu:**
```bash
sudo apt update
sudo apt install curl jq grep
```

**On macOS:**
```bash
brew install curl jq grep
```

**On Arch Linux:**
```bash
sudo pacman -S curl jq grep
```

**On Fedora/RHEL:**
```bash
sudo dnf install curl jq grep
```

---

## 📥 Installation

### Method 1: Clone the Repository

```bash
# Clone the repository
git clone https://github.com/yourusername/hunt-with-holmes.git

# Navigate to the directory
cd hunt-with-holmes

# Make the script executable
chmod +x hunt_holmes.sh
```

### Method 2: Direct Download

```bash
# Download the script
wget https://raw.githubusercontent.com/yourusername/hunt-with-holmes/main/hunt_holmes.sh

# Make it executable
chmod +x hunt_holmes.sh
```

---

## 🚀 Usage

### Basic Usage

```bash
./hunt_holmes.sh
```

The script will prompt you to enter a username:

```
[>] Input Username: john_doe
```

### Command Line Options

Currently, the script runs interactively. Future versions will include command-line arguments.

---

## 🌐 Platforms Covered

Hunt with Holmes checks the following 80+ platforms:

### Social Media
- Instagram
- Facebook
- Twitter (X)
- LinkedIn
- Reddit
- VK
- TikTok

### Professional Networks
- GitHub
- GitLab
- BitBucket
- Keybase
- AngelList
- Behance
- Dribbble

### Content Platforms
- YouTube
- Vimeo
- Twitch
- Medium
- Blogger
- WordPress
- Tumblr

### Creative Platforms
- DeviantART
- Flickr
- 500px
- Pinterest
- Designspiration

### Music & Audio
- Spotify
- SoundCloud
- Last.fm
- MixCloud
- Bandcamp
- ReverbNation

### Gaming
- Steam
- Roblox
- Kongregate
- Newgrounds

### Professional & Learning
- Codecademy
- CodeMentor
- Instructables
- HackerNews
- Wikipedia

### Lifestyle & Others
- About.me
- Patreon
- Pastebin
- Gravatar
- Foursquare
- TripAdvisor
- OkCupid
- Badoo
- GoodReads

**...and many more!**

---

## 📤 Output

### Console Output

The script provides real-time feedback with color-coded results:
- 🟢 **Green "Found!"** - Username exists on the platform
- 🟡 **Yellow "Not Found!"** - Username doesn't exist on the platform

### File Output

All found profiles are automatically saved to `[username].txt`:

```
https://www.instagram.com/john_doe
https://www.github.com/john_doe
https://www.reddit.com/user/john_doe
https://twitter.com/john_doe
...
```

---

## 💡 Examples

### Example 1: Basic Search

```bash
./hunt_holmes.sh
[>] Input Username: elonmusk
```

**Output:**
```
[>] Checking username elonmusk on social networks:
[+] Instagram: Found! https://www.instagram.com/elonmusk
[+] Facebook: Found! https://www.facebook.com/elonmusk
[+] Twitter: Found! https://www.twitter.com/elonmusk
...
[+] Saved: elonmusk.txt
```

### Example 2: Checking Compromised Data

The script also checks if the username appears in info-stealer databases:

```
[>] Checking username john_doe on global info-stealer:
[+] date compromised : 2023-05-15
[+] operating system : Windows 10
[+] computer name    : DESKTOP-ABC123
[+] ip address       : 192.168.1.100
```

---

## ⚖️ Legal Disclaimer

**IMPORTANT:** This tool is provided for educational and ethical purposes only.

- ✅ **Authorized Use**: Use only on accounts you own or have explicit permission to investigate
- ✅ **Security Research**: Legal penetration testing and authorized security assessments
- ✅ **OSINT Investigations**: Law enforcement and authorized investigations
- ❌ **Unauthorized Access**: Do not use for stalking, harassment, or unauthorized access
- ❌ **Privacy Violation**: Respect privacy laws and regulations in your jurisdiction

**By using this tool, you agree to:**
- Use it responsibly and ethically
- Comply with all applicable laws and regulations
- Not use it for malicious purposes
- Take full responsibility for your actions

The developers and contributors are not responsible for misuse of this tool.

---

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

### Adding New Platforms

1. Fork the repository
2. Add your platform check in the `scanner()` function:

```bash
## NewPlatform
printf "\e[1;77m[\e[0m\e[1;92m+\e[0m\e[1;77m] NewPlatform: \e[0m"
check1=$(curl -s -i "https://newplatform.com/$username" -H "Accept-Language: en" -L | grep -o 'HTTP/2 404' ; echo $?)

if [[ $check1 == *'0'* ]] ; then 
printf "\e[1;93mNot Found!\e[0m\n"
elif [[ $check1 == *'1'* ]]; then 
printf "\e[1;92m Found!\e[0m https://newplatform.com/%s\n" $username
printf "https://newplatform.com/%s\n" $username >> $username.txt
fi
```

3. Submit a pull request

### Reporting Issues

Found a bug? [Open an issue](https://github.com/yourusername/hunt-with-holmes/issues)

### Feature Requests

Have an idea? [Submit a feature request](https://github.com/yourusername/hunt-with-holmes/issues)

---

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2024 Hunt with Holmes Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.
```

---

## 📞 Contact

- **Issues**: [GitHub Issues](https://github.com/yourusername/hunt-with-holmes/issues)
- **Pull Requests**: [GitHub PRs](https://github.com/yourusername/hunt-with-holmes/pulls)
- **Discussions**: [GitHub Discussions](https://github.com/yourusername/hunt-with-holmes/discussions)

---

## 🌟 Star History

If you find this tool useful, please consider giving it a ⭐️!

---

## 📊 Statistics

![GitHub stars](https://img.shields.io/github/stars/yourusername/hunt-with-holmes?style=social)
![GitHub forks](https://img.shields.io/github/forks/yourusername/hunt-with-holmes?style=social)
![GitHub issues](https://img.shields.io/github/issues/yourusername/hunt-with-holmes)

---

## 🙏 Acknowledgments

- Inspired by various OSINT tools and frameworks
- Thanks to all contributors and the open-source community
- Special thanks to the cybersecurity research community

---

<div align="center">

**Made with ❤️ for the OSINT Community**

[⬆ Back to Top](#-hunt-with-holmes)

</div>