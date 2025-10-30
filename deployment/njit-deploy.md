# NJIT Server Deployment Guide

## Phase 1: Deploying to NJIT Server

### Prerequisites
- Access to NJIT web server (typically through NJIT's web hosting service)
- FTP/SFTP client or file manager access
- Basic understanding of web hosting

### Step 1: Prepare Files for Upload

1. **Compress your portfolio files**:
   - Create a ZIP file containing:
     - `index.html`
     - `styles.css`
     - `script.js`
     - `README.md`

2. **Verify file structure**:
   ```
   portfolio/
   ├── index.html
   ├── styles.css
   ├── script.js
   └── README.md
   ```

### Step 2: Access NJIT Web Server

1. **Log into NJIT's web hosting service**:
   - Usually accessible through NJIT's student portal
   - Look for "Web Hosting" or "Personal Web Space"

2. **Navigate to your web directory**:
   - Typically located at `/public_html/` or similar
   - This is your document root

### Step 3: Upload Files

1. **Upload via FTP/SFTP**:
   ```bash
   # Using SFTP (replace with your NJIT credentials)
   sftp username@web.njit.edu
   cd public_html
   put index.html
   put styles.css
   put script.js
   ```

2. **Or use NJIT's web file manager**:
   - Log into the web interface
   - Navigate to your web directory
   - Upload files using the interface

### Step 4: Set Permissions

1. **Set correct file permissions**:
   ```bash
   chmod 644 index.html
   chmod 644 styles.css
   chmod 644 script.js
   chmod 644 README.md
   ```

2. **Ensure directory permissions**:
   ```bash
   chmod 755 public_html
   ```

### Step 5: Test Your Website

1. **Access your portfolio**:
   - URL format: `https://web.njit.edu/~username/`
   - Replace `username` with your NJIT username

2. **Verify functionality**:
   - Test responsive design on different devices
   - Check all navigation links
   - Test contact form
   - Verify animations and interactions

### Step 6: Configure Domain (Optional)

1. **Custom domain setup**:
   - If NJIT allows custom domains
   - Update DNS settings to point to NJIT server
   - Configure virtual hosts if needed

### Troubleshooting

**Common Issues:**

1. **Files not displaying**:
   - Check file permissions (should be 644)
   - Verify files are in correct directory
   - Check for typos in filenames

2. **CSS/JS not loading**:
   - Verify file paths are correct
   - Check browser console for errors
   - Ensure files uploaded completely

3. **Contact form not working**:
   - NJIT server may not support PHP/backend processing
   - Consider using a third-party form service
   - Or implement client-side only validation

### Security Considerations

1. **File permissions**:
   - Never set files to 777 (full permissions)
   - Use 644 for files, 755 for directories

2. **HTTPS**:
   - NJIT typically provides SSL certificates
   - Ensure your site uses HTTPS

3. **Regular updates**:
   - Keep your portfolio updated
   - Monitor for any security advisories

### Performance Optimization

1. **Enable compression**:
   - Configure server to compress CSS/JS files
   - Use gzip compression if available

2. **Caching headers**:
   - Set appropriate cache headers for static assets
   - Use versioning for CSS/JS files

### Backup Strategy

1. **Regular backups**:
   - Keep local copies of all files
   - Use version control (Git) for tracking changes

2. **Documentation**:
   - Maintain deployment notes
   - Keep track of any custom configurations

### Next Steps

After successful NJIT deployment:
1. Test thoroughly across different browsers
2. Gather feedback from peers/instructors
3. Prepare for Phase 2: AWS deployment
4. Document any issues or customizations needed

### Support Resources

- NJIT IT Help Desk
- NJIT Web Hosting Documentation
- Student Portal Help Section
- NJIT Computer Science Department Resources
