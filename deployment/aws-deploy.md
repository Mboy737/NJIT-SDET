# AWS Deployment Guide

## Phase 2: Deploying to AWS

### Option 1: Amazon S3 Static Website Hosting

#### Prerequisites
- AWS Account (Free tier eligible)
- Basic understanding of AWS services
- Domain name (optional, but recommended)

#### Step 1: Create S3 Bucket

1. **Log into AWS Console**:
   - Navigate to S3 service
   - Click "Create bucket"

2. **Configure bucket settings**:
   ```
   Bucket name: your-portfolio-website (must be globally unique)
   Region: Choose closest to your audience
   Block public access: Uncheck "Block all public access"
   ```

3. **Enable static website hosting**:
   - Go to bucket Properties
   - Scroll to "Static website hosting"
   - Enable and set:
     - Index document: `index.html`
     - Error document: `index.html` (for SPA routing)

#### Step 2: Upload Files

1. **Upload portfolio files**:
   - Select all files (index.html, styles.css, script.js)
   - Set permissions to "Grant public read access"
   - Upload files

2. **Set bucket policy**:
   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Sid": "PublicReadGetObject",
         "Effect": "Allow",
         "Principal": "*",
         "Action": "s3:GetObject",
         "Resource": "arn:aws:s3:::your-bucket-name/*"
       }
     ]
   }
   ```

#### Step 3: Configure CloudFront (Optional but Recommended)

1. **Create CloudFront distribution**:
   - Origin Domain: Your S3 bucket website endpoint
   - Default Root Object: `index.html`
   - Price Class: Choose appropriate for your audience

2. **Configure caching**:
   - Set appropriate TTL values
   - Enable compression

### Option 2: AWS Amplify

#### Prerequisites
- AWS Account
- GitHub account (for automatic deployments)

#### Step 1: Connect Repository

1. **Create GitHub repository**:
   - Push your portfolio code to GitHub
   - Ensure proper file structure

2. **Connect to Amplify**:
   - Go to AWS Amplify console
   - Click "New app" → "Host web app"
   - Connect your GitHub repository

#### Step 2: Configure Build Settings

1. **Build specification** (amplify.yml):
   ```yaml
   version: 1
   frontend:
     phases:
       preBuild:
         commands:
           - echo "Installing dependencies"
       build:
         commands:
           - echo "Building the app"
     artifacts:
       baseDirectory: /
       files:
         - '**/*'
     cache:
       paths:
         - node_modules/**/*
   ```

2. **Deploy settings**:
   - Root directory: `/` (or your portfolio folder)
   - Build command: Leave empty for static site
   - Output directory: `/`

#### Step 3: Custom Domain (Optional)

1. **Add custom domain**:
   - Go to Domain Management in Amplify
   - Add your domain
   - Configure DNS settings

2. **SSL Certificate**:
   - Amplify automatically provisions SSL
   - Wait for certificate validation

### Option 3: AWS EC2 with Nginx

#### Prerequisites
- AWS Account
- Basic Linux knowledge
- EC2 instance (t2.micro for free tier)

#### Step 1: Launch EC2 Instance

1. **Choose AMI**:
   - Select Ubuntu Server 20.04 LTS
   - Choose t2.micro (free tier eligible)

2. **Configure security group**:
   - Allow HTTP (port 80)
   - Allow HTTPS (port 443)
   - Allow SSH (port 22) from your IP

#### Step 2: Install Nginx

1. **Connect to instance**:
   ```bash
   ssh -i your-key.pem ubuntu@your-instance-ip
   ```

2. **Install Nginx**:
   ```bash
   sudo apt update
   sudo apt install nginx
   sudo systemctl start nginx
   sudo systemctl enable nginx
   ```

#### Step 3: Deploy Website

1. **Upload files**:
   ```bash
   # Create website directory
   sudo mkdir -p /var/www/portfolio
   
   # Upload files (use SCP or SFTP)
   scp -i your-key.pem index.html ubuntu@your-instance-ip:/tmp/
   scp -i your-key.pem styles.css ubuntu@your-instance-ip:/tmp/
   scp -i your-key.pem script.js ubuntu@your-instance-ip:/tmp/
   
   # Move files to web directory
   sudo mv /tmp/*.html /var/www/portfolio/
   sudo mv /tmp/*.css /var/www/portfolio/
   sudo mv /tmp/*.js /var/www/portfolio/
   ```

2. **Configure Nginx**:
   ```bash
   sudo nano /etc/nginx/sites-available/portfolio
   ```
   
   Add configuration:
   ```nginx
   server {
       listen 80;
       server_name your-domain.com www.your-domain.com;
       root /var/www/portfolio;
       index index.html;
       
       location / {
           try_files $uri $uri/ =404;
       }
   }
   ```

3. **Enable site**:
   ```bash
   sudo ln -s /etc/nginx/sites-available/portfolio /etc/nginx/sites-enabled/
   sudo nginx -t
   sudo systemctl reload nginx
   ```

### Performance Optimization

#### 1. Enable Compression
```nginx
# Add to Nginx config
gzip on;
gzip_vary on;
gzip_min_length 1024;
gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;
```

#### 2. Set Cache Headers
```nginx
# Add to Nginx config
location ~* \.(css|js|png|jpg|jpeg|gif|ico|svg)$ {
    expires 1y;
    add_header Cache-Control "public, immutable";
}
```

#### 3. Use CDN
- CloudFront for AWS
- Consider CloudFlare for additional features

### Security Best Practices

#### 1. HTTPS Configuration
```bash
# Install Certbot for Let's Encrypt
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d your-domain.com
```

#### 2. Security Headers
```nginx
# Add to Nginx config
add_header X-Frame-Options "SAMEORIGIN" always;
add_header X-XSS-Protection "1; mode=block" always;
add_header X-Content-Type-Options "nosniff" always;
add_header Referrer-Policy "no-referrer-when-downgrade" always;
add_header Content-Security-Policy "default-src 'self' http: https: data: blob: 'unsafe-inline'" always;
```

#### 3. Firewall Configuration
```bash
# Configure UFW
sudo ufw allow 22
sudo ufw allow 80
sudo ufw allow 443
sudo ufw enable
```

### Monitoring and Maintenance

#### 1. Set Up Monitoring
- CloudWatch for AWS services
- Monitor uptime and performance
- Set up alerts for downtime

#### 2. Regular Updates
- Keep server packages updated
- Monitor security advisories
- Regular backups

#### 3. Cost Optimization
- Use AWS Cost Explorer
- Set up billing alerts
- Optimize resource usage

### Troubleshooting

#### Common Issues:

1. **403 Forbidden**:
   - Check file permissions
   - Verify Nginx configuration
   - Check SELinux status

2. **502 Bad Gateway**:
   - Check Nginx error logs
   - Verify service status
   - Check port configuration

3. **SSL Issues**:
   - Verify certificate installation
   - Check certificate expiration
   - Validate domain configuration

### Cost Estimation

#### S3 + CloudFront (Recommended):
- S3: ~$0.023 per GB stored
- CloudFront: ~$0.085 per GB transferred
- Total: ~$1-5/month for typical portfolio

#### EC2 + Nginx:
- t2.micro: Free tier (750 hours/month)
- Data transfer: ~$0.09 per GB
- Total: ~$0-10/month depending on traffic

### Next Steps

After successful AWS deployment:
1. Test all functionality
2. Set up monitoring
3. Configure custom domain
4. Implement CI/CD pipeline
5. Document deployment process
6. Plan for scaling if needed

### Support Resources

- AWS Documentation
- AWS Support (if on paid plan)
- AWS Community Forums
- Stack Overflow (AWS tags)
- AWS re:Post community
