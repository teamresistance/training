# Team Resistance #86 - Programming Training Website

A complete static HTML training website for new programmers featuring all documentation, visual tools, and resources.

## Overview

A **complete programming training system** for Team Resistance, including:

- Full website with all materials
- Skill-based curriculum (no time constraints)
- Team Resistance branded throughout (green theme)
- Ready to deploy and use immediately

## Quick Start

### Viewing the Website

Simply open `index.html` in your web browser. All pages are static HTML and work without any server or build process.

**Option 1: Direct File Opening**
```bash
# Navigate to the repository folder
cd /path/to/challenges

# Open in your default browser (Mac/Linux)
open index.html

# Or on Windows
start index.html
```

**Option 2: Drag and Drop**
Drag the `index.html` file into any web browser window.

## Website Structure

```
challenges/
├── index.html              # Home page
├── challenges.html         # All 6 programming challenges
├── mentor-guide.html       # Guide for mentors
├── quick-reference.html    # Quick reference cheat sheet
├── progression.html        # Visual skills progression
├── tracker.html            # Printable challenge tracker
├── styles.css              # Centralized Team Resistance styling
└── README.md               # This file
```

## Features

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
- Learning goals
- Resource links

#### **Mentor Guide (mentor-guide.html)**
- Challenge-by-challenge teaching notes
- Common student struggles
- Debugging help
- Assessment templates

#### **Quick Reference (quick-reference.html)**
- FRC programming essentials
- PID tuning guide
- Motor control basics
- Command-based architecture
- Debugging checklists

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

## Challenge Overview

| Challenge                     | Difficulty          | Skills                       |
| ----------------------------- | ------------------- | ---------------------------- |
| **1: Motor Control**          | ⭐ Beginner         | Basic control, safety limits |
| **2: Sensors & Telemetry**    | ⭐⭐ Beginner-Int   | Encoders, SmartDashboard     |
| **3: PID Control**            | ⭐⭐⭐ Intermediate | PID tuning, motion control   |
| **4: Subsystem Architecture** | ⭐⭐⭐ Intermediate | Commands, subsystems         |
| **5: Autonomous Routine**     | ⭐⭐⭐⭐ Advanced   | Command groups, sequencing   |
| **6: Integration Project**    | ⭐⭐⭐⭐⭐ Advanced | Multi-subsystem, safety      |

**Plus 4 bonus challenges** for advanced programmers!

## Hosting Options

### Option 1: GitHub Pages (Free)

1. Create a GitHub repository
2. Upload all files to the repository
3. Enable GitHub Pages in repository settings
4. Access at: `https://yourusername.github.io/repository-name`

### Option 2: Team Server

- Upload to your team's web server
- Point a subdomain (e.g., `training.teamresistance.org`)
- Ensure all files are uploaded

### Option 3: USB Drive / Local Network

- Copy folder to USB or network drive
- Team members can open `index.html` directly in browsers
- Works offline!

## Customization

### Updating Colors

Edit `styles.css` and change the root variables:

```css
:root {
  --resistance-green: #00ff41; /* Change your primary color */
  --resistance-green-dark: #00cc33;
  /* ... more colors */
}
```

All colors update automatically throughout the site!

### Updating Team Info

Search and replace in all files:

- Team number: "86" → your team number
- City: "Jacksonville, FL" → your location
- Year: "1996" → your founding year
- "TEAM RESISTANCE" → your team name

### Adding New Pages

1. Copy the structure from any existing HTML file
2. Update the `<title>` and content
3. Add link to sidebar navigation in all files
4. Use same header/footer/navigation structure

## Technical Details

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

## Training Philosophy

### Key Principles

1. **Skill-Based** - No arbitrary timelines
2. **Hands-On** - Real robot hardware
3. **Mentorship** - 1:1 support
4. **Competition-Ready** - Directly applicable

### For New Programmers

1. Start at home page
2. View progression path
3. Print challenge tracker
4. Bookmark quick reference
5. Work through challenges page

### For Mentors

1. Review mentor guide first
2. Use during mentoring sessions
3. Reference common struggles section
4. Use assessment templates

### For Team Leads

1. Display on monitors during recruitment
2. Send link to new members
3. Use in presentations
4. Track team progress

## External Resources

- [Team GitHub](https://github.com/teamresistance)
- [The Blue Alliance](https://www.thebluealliance.com/team/86)
- [WPILib Documentation](https://docs.wpilib.org)
- [REV Robotics Docs](https://docs.revrobotics.com)
- [Chief Delphi Forums](https://www.chiefdelphi.com)

## Team Resistance

**FRC Team #86**
Jacksonville, Florida
**Going against the current since 1996!**

This training system represents nearly 30 years of robotics programming excellence. Use it to train the next generation of programmers who will carry on the legacy.

## License

Created for FRC Team 86 - Team Resistance
Free to use and modify for educational purposes
Share with other FRC teams!

---

_Questions or issues? Contact your programming sub-team lead._
