# Project Images

This folder contains images for the projects displayed on the portfolio website.

## Required Images

To display project images properly, add the following images to this folder:

### 1. EMS Operations
- **File**: `ems-operations.jpg`
- **Description**: Image showing Keyport First Aid volunteer EMT operations, ambulances, or emergency medical services
- **Recommended size**: 400x300px (4:3 aspect ratio)
- **Alt text**: "Keyport First Aid - Volunteer EMT Emergency Medical Services"

### 2. Radio Programming
- **File**: `radio-programming.jpg`
- **Description**: Image showing Motorola radio equipment, communication systems, or radio programming
- **Recommended size**: 400x300px (4:3 aspect ratio)
- **Alt text**: "Motorola Radio Programming - Communication Systems"

### 3. Vehicle Technician
- **File**: `vehicle-technician.jpg`
- **Description**: Image showing emergency vehicles, maintenance work, or vehicle equipment
- **Recommended size**: 400x300px (4:3 aspect ratio)
- **Alt text**: "Emergency Vehicle Technician - Maintenance and Repair"

## Image Guidelines

- **Format**: JPG or PNG
- **Aspect Ratios**: 
  - **Desktop**: 4:3 (400x300px recommended)
  - **Tablet**: 16:9 (will auto-adjust)
  - **Mobile**: 1:1 (square format)
- **Quality**: High resolution for crisp display
- **Content**: Professional, relevant to the project
- **Optimization**: Compress images for web performance
- **Centering**: Images will automatically center themselves
- **Scaling**: Images will scale to fit the container while maintaining aspect ratio

## Responsive Behavior

The project images will automatically adjust their aspect ratio based on screen size:

- **Desktop (768px+)**: 4:3 aspect ratio
- **Tablet (480px-768px)**: 16:9 aspect ratio  
- **Mobile (under 480px)**: 1:1 (square) aspect ratio

## Fallback

If images are not available, the project cards will display with a gradient background. The images will automatically scale, center, and maintain aspect ratio when added.

## Adding New Projects

To add a new project with an image:

1. Add the image file to this folder
2. Update the `src` attribute in the HTML to point to your image
3. Update the `alt` attribute with descriptive text
4. Ensure the image follows the size guidelines above
5. The image will automatically center and scale appropriately
