from pathlib import Path
import re

src = Path("/mnt/data/README_animated.md")
text = src.read_text(encoding="utf-8")

# Simplify the top animation and remove the unneeded trophy, streak, and contribution activity widgets.
text = re.sub(
    r'<!-- Animated hero -->.*?</div>\n\n---',
    '''<!-- Clean animated hero -->
<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=700&size=27&duration=3200&pause=1000&color=22D3EE&center=true&vCenter=true&width=720&height=65&lines=Hi%2C+I'm+Mayank+Soam+%F0%9F%91%8B;CSIT+Student+%7C+Aspiring+Developer;Learning.+Building.+Improving." alt="Animated introduction for Mayank Soam" />

<p><em>Curious mind. Practical projects. Continuous growth.</em></p>

<p>
  <a href="https://github.com/mayank188?tab=followers"><img src="https://img.shields.io/github/followers/mayank188?label=Followers&style=flat-square&color=7C3AED" alt="GitHub followers" /></a>
  <img src="https://komarev.com/ghpvc/?username=mayank188&label=Profile%20views&color=0891B2&style=flat-square" alt="Profile views" />
  <a href="https://linkedin.com/in/mayank-soam-b68946339"><img src="https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
  <a href="mailto:mayanksom36@gmail.com"><img src="https://img.shields.io/badge/Email-Contact-EA4335?style=flat-square&logo=gmail&logoColor=white" alt="Email" /></a>
</p>

</div>

---''',
    text,
    count=1,
    flags=re.S
)

# Remove analytics streak card, contribution graph and trophy sections; retain only the basic stats and languages.
text = re.sub(
    r'\n<a href="https://github\.com/mayank188">\n  <img height="175" src="https://github-readme-streak-stats\.herokuapp\.com/.*?</a>\n\n</div>',
    '\n</div>',
    text,
    count=1,
    flags=re.S
)
text = re.sub(
    r'\n## 📈 Contribution Activity.*?(?=\n---|\n## 🚀 Featured Project)',
    '',
    text,
    count=1,
    flags=re.S
)
text = re.sub(
    r'\n## 🏆 GitHub Trophies.*?(?=\n---|\n## 🚀 Featured Project)',
    '',
    text,
    count=1,
    flags=re.S
)

# Replace overly detailed project copy with a short, honest project card.
text = re.sub(
    r'## 🚀 Featured Project.*?(?=\n---\n\n## 🌐 Find Me Online)',
    '''## 🚀 Featured Project

<div align="center">

### [Github-Analyser](https://github.com/mayank188/Github-Analyser-)

A project I'm working on. Visit the repository to explore the current code and features.

<a href="https://github.com/mayank188/Github-Analyser-">
  <img src="https://img.shields.io/badge/View%20Repository-7C3AED?style=for-the-badge&logo=github&logoColor=white" alt="View Github-Analyser repository" />
</a>

</div>

> Add a verified project summary, tech stack, and demo link when those details are ready.''',
    text,
    count=1,
    flags=re.S
)

# Keep only one animated message at the end, shorter and cleaner.
text = re.sub(
    r'<img src="https://readme-typing-svg\.demolab\.com\?font=Fira\+Code&weight=500&size=18.*?alt="Animated closing message" />',
    '<img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=600&size=17&duration=3500&pause=1200&color=22D3EE&center=true&vCenter=true&width=520&height=38&lines=Thanks+for+visiting!+%E2%9C%A8;Let's+build+something+useful." alt="Animated closing message" />',
    text,
    count=1,
    flags=re.S
)

# Minor copy cleanup and reduce crowded skill icon rows.
text = text.replace(
    '<img src="https://skillicons.dev/icons?i=c,cpp,python,java,javascript,typescript" alt="C, C++, Python, Java, JavaScript, and TypeScript" />',
    '<img src="https://skillicons.dev/icons?i=c,cpp,python,javascript" alt="C, C++, Python, and JavaScript" />'
)
text = text.replace(
    '<img src="https://skillicons.dev/icons?i=nodejs,express,mongodb,mysql,firebase" alt="Node.js, Express, MongoDB, MySQL, and Firebase" />',
    '<img src="https://skillicons.dev/icons?i=nodejs,express,mongodb,mysql,firebase" alt="Node.js, Express, MongoDB, MySQL, and Firebase" />'
)
text = text.replace(
    '## 📊 GitHub Analytics\n',
    '## 📊 GitHub Snapshot\n'
)

out = Path("/mnt/data/README_clean_animated.md")
out.write_text(text, encoding="utf-8")
print(f"Created {out} ({len(text.splitlines())} lines, {out.stat().st_size} bytes)")
