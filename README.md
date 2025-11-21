# Team Resistance #86 - Programming Training Website

A complete training website for new programmers featuring all documentation, visual tools, and resources.

---

## 🌊⚡ Quick Start

### View the Website Locally

**Option 1: Python (Recommended)**

```bash
# Navigate to the website folder
cd website

# Start a local web server (Python 3)
python3 -m http.server 8000

# Open your browser to:
# http://localhost:8000
```

**Option 2: Using launch scripts**

```bash
# On Windows:
double-click launch_server.bat

# On Mac/Linux:
./launch_server.sh
```

---

## 📁 Website Structure

```
website/
├── index.html              # Home page
├── challenges.html         # All 6 programming challenges
├── mentor-guide.html       # Guide for mentors
├── quick-reference.html    # Quick reference cheat sheet
├── progression.html        # Visual skills progression
├── tracker.html            # Printable challenge tracker
├── styles.css              # Centralized Team Resistance styling
├── README.md               # This file
└── launch_server.*         # Helper scripts to start local server
```

---

## 🎨 Features

### Consistent Navigation

- **Header Navigation**: Quick access to main pages
- **Sidebar Navigation**: Full site map with sections
- **Mobile Responsive**: Works on phones and tablets
- **Team Resistance Branding**: Green theme throughout

### Pages

#### **Home (index.html)**

- Welcome and overview
- Quick stats
- Links to all sections
- Team philosophy

#### **Challenges (challenges.html)**

- All 6 core programming challenges
- Detailed requirements
- Success criteria
- Resource links

#### **Mentor Guide (mentor-guide.html)**

- Challenge-by-challenge teaching notes
- Common student struggles
- Debugging help
- Assessment templates

#### **Quick Reference (quick-reference.html)**

- FRC programming essentials
- PID tuning guide
- Common debugging scenarios
- Code snippets

#### **Skills Progression (progression.html)**

- Interactive visual roadmap
- Animated challenge cards
- Hover effects
- Skills breakdown

#### **Challenge Tracker (tracker.html)**

- Printable progress sheet
- Checkboxes for each challenge
- Requirements checklist
- Signature section

---

## 🚀 Hosting Options

### Option 1: GitHub Pages (Free)

1. Create a GitHub repository
2. Upload the `website` folder contents
3. Enable GitHub Pages in repository settings
4. Access at: `https://yourusername.github.io/repository-name`

### Option 2: Team Server

- Upload to your team's web server
- Point a subdomain (e.g., `training.teamresistance.org`)
- Ensure all files are uploaded

### Option 3: USB Drive / Local Network

- Copy `website` folder to USB or network drive
- Team members can open `index.html` directly in browsers
- Works offline!

---

## 💡 Customization

### Updating Colors

Edit `styles.css` and change the root variables:

```css
:root {
  --resistance-green: #00ff41; /* Change your primary color */
  --resistance-green-dark: #00cc33;
  /* ... more colors */
}
```

### Adding Content

- Markdown files in `/mnt/user-data/outputs/` can be converted to HTML
- Follow the same template structure
- Add navigation links to all pages

### Updating Team Info

Search and replace:

- Team number: "86" → your team number
- City: "Jacksonville, FL" → your location
- Year: "2025" → current season

---

## 📱 Mobile Support

The website is fully responsive:

- **Desktop**: Full sidebar + header navigation
- **Tablet**: Collapsible sidebar
- **Mobile**: Hamburger menu (☰)

---

## 🎓 For Programming Leads

### Before Launching

- [ ] Review all content for accuracy
- [ ] Update team-specific links
- [ ] Test on different devices
- [ ] Print the tracker page for distribution

### During Onboarding

1. Show new members the home page
2. Walk through the progression visual
3. Give them the tracker (print or digital)
4. Assign Challenge 1

### Maintenance

- Update challenge completion stats
- Add team success stories
- Link to new GitHub repositories
- Update for each season

---

## 🔗 External Resources Linked

- [Team GitHub](https://github.com/teamresistance)
- [The Blue Alliance](https://www.thebluealliance.com/team/86)
- [WPILib Documentation](https://docs.wpilib.org)
- [REV Robotics Docs](https://docs.revrobotics.com)
- [Chief Delphi Forums](https://www.chiefdelphi.com)

---

## ⚙️ Technical Details

**Built With:**

- Pure HTML5
- CSS3 (with CSS Variables)
- Vanilla JavaScript (no frameworks)
- Mobile-first responsive design

**Browser Support:**

- Chrome/Edge (recommended)
- Firefox
- Safari
- Mobile browsers

**No Dependencies:**

- No npm/node required
- No build process
- No external libraries
- Works offline

---

## 📝 License & Usage

Created for FRC Team 86 - Team Resistance
Free to use and modify for educational purposes
Attribution appreciated but not required

---

## 🤝 Contributing

To add new content:

1. Create markdown files following existing format
2. Convert to HTML using the template structure
3. Add navigation links
4. Test responsiveness

---

## 🌊⚡ Team Resistance

**FRC #86**  
Jacksonville, Florida  
Going against the current since 1996!

---

_Need help? Contact your programming sub-team lead._
