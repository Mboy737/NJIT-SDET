# Portfolio Testing Checklist

## Quick Testing Steps

### 1. Basic Functionality Test
- [ ] Page loads without errors
- [ ] Navigation menu works (click each link)
- [ ] Mobile hamburger menu toggles properly
- [ ] Smooth scrolling between sections
- [ ] All sections display correctly

### 2. Interactive Elements Test
- [ ] Contact form validation works
- [ ] Try submitting empty form (should show errors)
- [ ] Try submitting with invalid email (should show error)
- [ ] Try submitting valid form (should show success message)
- [ ] Skills progress bars animate when scrolling to skills section
- [ ] Project cards have hover effects

### 3. Responsive Design Test
- [ ] Desktop view (1200px+)
- [ ] Tablet view (768px - 1199px)
- [ ] Mobile view (320px - 767px)
- [ ] Test on actual mobile device if possible

### 4. Browser Compatibility Test
- [ ] Chrome
- [ ] Firefox
- [ ] Edge
- [ ] Safari (if available)

### 5. Performance Test
- [ ] Page loads quickly
- [ ] Animations are smooth
- [ ] No console errors (F12 → Console tab)

## Testing Commands

### Open in Browser
```bash
# Navigate to your portfolio folder
cd "c:\Users\adamp\OneDrive\Desktop\NJIT File Submissions\NJIT SDET"

# Open in default browser
start index.html
```

### Local Server (Optional - for advanced testing)
```bash
# Python server (if Python installed)
python -m http.server 8000
# Then visit: http://localhost:8000

# Node.js server (if Node.js installed)
npx serve .
# Then visit the provided URL
```

## Common Issues to Check

### CSS Issues
- Check if styles are loading (F12 → Network tab)
- Verify file paths in HTML
- Check for CSS syntax errors

### JavaScript Issues
- Open browser console (F12 → Console)
- Look for any red error messages
- Test all interactive features

### Responsive Issues
- Use browser dev tools (F12 → Toggle device toolbar)
- Test different screen sizes
- Check mobile navigation

## Quick Fix Commands

### Clear Browser Cache
- Chrome: Ctrl + Shift + Delete
- Firefox: Ctrl + Shift + Delete
- Edge: Ctrl + Shift + Delete

### Hard Refresh
- Ctrl + F5 (Windows)
- Cmd + Shift + R (Mac)

### Developer Tools
- F12 (most browsers)
- Right-click → Inspect Element
- Ctrl + Shift + I (Chrome/Edge)
