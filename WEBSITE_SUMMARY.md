# Team Resistance #86 - Programming Training Website

## Complete Package Summary

---

## 🎉 What You Have

A **fully functional, themed website** containing all your programming training materials with:

- ✅ Consistent Team Resistance branding (green theme)
- ✅ Responsive navigation (works on mobile/tablet/desktop)
- ✅ All markdown documents converted to HTML
- ✅ Visual tools integrated
- ✅ Ready to host or use locally

---

## 📂 Complete File List

### In `/website/` folder:

#### **HTML Pages (7 pages)**

1. **index.html** - Home page with overview and quick links
2. **challenges.html** - All 6 programming challenges (converted from markdown)
3. **mentor-guide.html** - Complete mentor guide (converted from markdown)
4. **quick-reference.html** - Programming reference sheet (converted from markdown)
5. **progression.html** - Interactive visual skills progression path
6. **tracker.html** - Printable challenge tracker/certificate
7. **README.md** - Website documentation and instructions

#### **Styling**

- **styles.css** - Centralized Team Resistance theme
  - Green color scheme (#00ff41)
  - Responsive design
  - Consistent typography
  - Reusable components

#### **Launch Scripts**

- **launch_server.bat** - Windows one-click server launch
- **launch_server.sh** - Mac/Linux server launch script

---

## 🚀 How to Use

### View Locally (Easiest)

**Windows:**

```
1. Navigate to the website folder
2. Double-click launch_server.bat
3. Open browser to http://localhost:8000
```

**Mac/Linux:**

```
1. Open Terminal
2. cd to website folder
3. ./launch_server.sh
4. Open browser to http://localhost:8000
```

**Manual Method:**

```bash
cd website
python3 -m http.server 8000
# Then open http://localhost:8000 in browser
```

### Host Online

**GitHub Pages (Free):**

1. Create GitHub repo
2. Upload website folder contents to root
3. Settings → Pages → Enable
4. Site live at `https://yourusername.github.io/repo-name`

**Team Server:**

- Upload to your team's web hosting
- All files in website folder
- Point DNS to location

---

## 🎨 Design Features

### Navigation System

- **Fixed Header**: Logo, team name, main nav links
- **Sidebar**: Full navigation menu with sections
- **Mobile Menu**: Hamburger menu (☰) for small screens
- **Active States**: Current page highlighted

### Color Scheme

```css
Primary Green: #00ff41 (Team Resistance brand)
Dark Green:    #00cc33
Light Green:   #00ff88
Background:    #1a1a1a (dark)
Text:          #cccccc (light gray)
Accents:       Green glows and shadows
```

### Responsive Breakpoints

- **Desktop (>1024px)**: Full sidebar + header
- **Tablet (768-1024px)**: Collapsible sidebar
- **Mobile (<768px)**: Hamburger menu, optimized text sizes

---

## 📄 Page Descriptions

### Home (index.html)

**Purpose:** Landing page and overview  
**Content:**

- Team logo and branding
- Quick statistics (29 years, 6 challenges, etc.)
- Training philosophy cards
- Quick action buttons
- Minimal content, focuses on navigation

### Challenges (challenges.html)

**Purpose:** Main curriculum document  
**Content:**

- All 6 challenges with full details
- Requirements and objectives
- Success criteria
- Learning goals
- Resource links
- Converted from: `Team86_Beginner_Programming_Challenges.md`

### Mentor Guide (mentor-guide.html)

**Purpose:** Mentor training and support  
**Content:**

- Teaching strategies by challenge
- Common struggles and solutions
- Red flags to watch for
- Debugging tips
- Assessment templates
- Converted from: `Team86_Mentor_Guide.md`

### Quick Reference (quick-reference.html)

**Purpose:** Printable/bookmark-able reference  
**Content:**

- FRC programming essentials
- PID tuning guide
- Motor control basics
- Command-based architecture
- Debugging checklists
- Converted from: `Team86_Quick_Reference.md`

### Skills Progression (progression.html)

**Purpose:** Visual journey map  
**Content:**

- Interactive challenge cards
- Animated path visualization
- Skills breakdown per challenge
- Hover effects and animations
- Motivational design

### Challenge Tracker (tracker.html)

**Purpose:** Progress tracking and certification  
**Content:**

- Checkboxes for each challenge
- Requirements lists
- Signature section for completion
- Printable format
- Can serve as certificate

---

## 💻 Technical Specifications

### Technologies Used

- **HTML5** - Modern semantic markup
- **CSS3** - CSS Variables, Flexbox, Grid
- **Vanilla JavaScript** - No frameworks needed
- **No Build Process** - Works immediately

### Browser Compatibility

✅ Chrome/Edge (Recommended)  
✅ Firefox  
✅ Safari  
✅ Mobile browsers (iOS Safari, Chrome Mobile)

### File Size

- Total: ~150KB (very lightweight!)
- No external dependencies
- Works 100% offline
- Fast load times

### Accessibility

- Semantic HTML structure
- Proper heading hierarchy
- Keyboard navigation support
- High contrast (dark theme)
- Mobile-friendly tap targets

---

## 🔧 Customization Guide

### Change Team Colors

Edit `styles.css` line 4-12:

```css
:root {
  --resistance-green: #00ff41; /* Your color here */
  --resistance-green-dark: #00cc33;
  /* etc... */
}
```

All colors update automatically throughout the site!

### Update Team Info

Search and replace in all files:

- "86" → Your team number
- "Jacksonville, FL" → Your location
- "1996" → Your founding year
- "TEAM RESISTANCE" → Your team name

### Add New Pages

1. Copy the structure from any existing HTML file
2. Update the `<title>` and content
3. Add link to sidebar navigation in all files
4. Use same header/footer/navigation structure

---

## 📱 Mobile Features

- Responsive images and layouts
- Touch-friendly buttons (44px+ targets)
- Collapsible navigation
- Readable text sizes (no tiny fonts)
- Tested on iOS and Android

---

## 🎯 Usage Scenarios

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

---

## 📊 Success Metrics

After deployment, you can track:

- How many students complete challenges
- Which challenges are most difficult
- Time spent on each page (if you add analytics)
- Mobile vs desktop usage

---

## 🔄 Maintenance

### Regular Updates

- [ ] Update for each competition season
- [ ] Add new challenges as developed
- [ ] Update team GitHub links
- [ ] Add success stories/testimonials

### Content Refresh

- Keep challenge requirements current
- Update WPILib version references
- Add new resources as discovered
- Update team achievements

---

## 🎓 Educational Value

This website teaches:

- **Programming skills** (primary goal)
- **Documentation** (well-structured content)
- **Web design** (if students want to customize)
- **Version control** (if hosted on GitHub)
- **Professional presentation** (portfolio piece)

---

## 🏆 Advantages Over Other Formats

**vs. Google Docs:**

- ✅ More professional looking
- ✅ Better navigation
- ✅ Offline capable
- ✅ No sign-in required

**vs. PDFs:**

- ✅ Interactive (clickable links)
- ✅ Searchable
- ✅ Responsive to screen size
- ✅ Easy to update

**vs. Notion/Confluence:**

- ✅ No account required
- ✅ No subscription
- ✅ Full control/customization
- ✅ Works offline

---

## 📦 What's Included vs What's Not

### ✅ Included

- All documentation
- Visual tools
- Navigation system
- Responsive design
- Launch scripts
- README files

### ❌ Not Included (Optional Additions)

- Search functionality (can add with JavaScript)
- Analytics tracking (can add Google Analytics)
- User accounts/login
- Database backend
- Comments system
- Auto-deployment

---

## 🚨 Important Notes

1. **No Server Required**: Just HTML/CSS/JS files
2. **No Installation**: Works immediately
3. **No Dependencies**: Zero npm packages
4. **Version Control Friendly**: All text files
5. **Easy to Share**: Just zip and send

---

## 📞 Support & Questions

For issues with:

- **Website structure**: Check README.md in website folder
- **Content accuracy**: Review original markdown files
- **Hosting**: See hosting section above
- **Customization**: CSS is well-commented

---

## 🌟 Next Steps

1. **Review the website**: Launch locally and browse all pages
2. **Customize**: Update team-specific information
3. **Test**: Try on different devices
4. **Deploy**: Choose hosting method
5. **Share**: Send link to team members
6. **Iterate**: Gather feedback and improve

---

## 🎨 Design Credits

**Theme:** Team Resistance Green (#00ff41)  
**Inspiration:** FRC team websites, modern documentation sites  
**Layout:** Sidebar navigation with fixed header  
**Icons:** Unicode emojis for universal support

---

## 📜 Version History

**v1.0 - 2025 Season**

- Initial release
- 6 core challenges
- All documentation pages
- Visual tools
- Fully responsive design

---

## 🌊⚡ Final Note

This website represents nearly 30 years of Team Resistance excellence in robotics programming. Use it to train the next generation of programmers who will continue going against the current!

**Team Resistance #86**  
Jacksonville, Florida  
Since 1996

---

_Questions? Contact your programming sub-team lead._
