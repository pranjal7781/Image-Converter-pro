# Image Converter Pro 🖼️

A modern, web-based image conversion tool built with Flask and featuring a beautiful, responsive UI. Convert your images to various formats including JPG, PNG, SVG, PDF, and DOCX with ease.

![Image Converter Pro](https://img.shields.io/badge/Python-3.7+-blue.svg)
![Flask](https://img.shields.io/badge/Flask-2.0+-green.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

## ✨ Features

- **Multiple Format Support**: Convert images to JPG, PNG, SVG, PDF, and DOCX
- **Drag & Drop Interface**: Intuitive file upload with drag-and-drop functionality
- **Real-time Preview**: See your image before conversion
- **Responsive Design**: Works perfectly on desktop and mobile devices
- **Modern UI**: Beautiful glassmorphism design with smooth animations
- **File Management**: Automatic cleanup of temporary files
- **Error Handling**: Comprehensive error handling and user feedback
- **Secure Upload**: File validation and secure filename handling

## 🚀 Quick Start

### Prerequisites

- Python 3.7 or higher
- pip (Python package installer)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/image-converter-pro.git
   cd image-converter-pro
   ```

2. **Create a virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: python -m venv venv
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run the application**
   ```bash
   python app.py
   ```

5. **Open your browser**
   Navigate to `http://localhost:5000`

## 📦 Dependencies

Create a `requirements.txt` file with the following dependencies:

```

Flask==2.3.3
Pillow==10.0.1
reportlab==4.0.4
python-docx==0.8.11
svgwrite==1.4.3
Werkzeug==2.3.7
```

## 🏗️ Project Structure

```
image-converter-pro/
│
├── app.py                 # Main Flask application
├── templates/
│   └── index.html        # Frontend HTML template
├── uploads/              # Temporary upload directory
├── outputs/              # Converted files directory
├── requirements.txt      # Python dependencies
└── README.md            # Project documentation
```

## 🎯 Usage

1. **Upload an Image**
   - Click the upload area or drag and drop an image file
   - Supported formats: PNG, JPG, JPEG, GIF, BMP, TIFF, WebP

2. **Choose Output Format**
   - Select from available formats: JPG, PNG, SVG, PDF, DOCX
   - Each format is optimized for different use cases

3. **Convert & Download**
   - Click "Convert Image" button
   - Download the converted file automatically

## 🔧 Configuration

### File Size Limits
The application supports files up to **16MB** by default. To change this:

```python
app.config['MAX_CONTENT_LENGTH'] = 32 * 1024 * 1024  # 32MB
```

### Directory Structure
The app creates two directories:
- `uploads/`: Stores temporary uploaded files
- `outputs/`: Stores converted files

### Security Settings
Update the secret key in production:

```python
app.secret_key = 'your-secure-secret-key-here'
```

## 🔄 API Endpoints

### Upload Image
```http
POST /upload
Content-Type: multipart/form-data

Response: JSON with file information
```

### Convert Image
```http
POST /convert
Content-Type: application/json

Body:
{
  "filename": "uploaded_filename",
  "format": "target_format"
}
```

### Download File
```http
GET /download/<filename>
```

### Cleanup Files
```http
GET /cleanup
```

## 🎨 Supported Conversions

| From Format | To Format | Quality | Notes |
|-------------|-----------|---------|-------|
| Any Image   | JPG       | High    | Lossy compression, white background for transparency |
| Any Image   | PNG       | Lossless| Preserves transparency |
| Any Image   | SVG       | Vector  | Embeds as base64 image |
| Any Image   | PDF       | High    | Scaled to fit page, centered |
| Any Image   | DOCX      | High    | Embedded in Word document |

## 🛠️ Development

### Running in Development Mode
```bash
python app.py
```
The app runs with debug mode enabled and auto-reload.

### Production Deployment
For production deployment:

1. Set debug mode to False
2. Use a production WSGI server like Gunicorn
3. Configure proper file permissions
4. Set up automated cleanup for temporary files

### Environment Variables
```bash
export FLASK_ENV=production
export SECRET_KEY=your-production-secret-key
```

## 🔒 Security Considerations

- Files are validated for allowed extensions
- Filenames are secured using `werkzeug.utils.secure_filename`
- Unique filenames prevent conflicts
- Automatic cleanup prevents disk space issues
- File size limits prevent abuse

## 🧹 File Cleanup

The application includes an automatic cleanup endpoint that removes files older than 1 hour. In production, set up a cron job:

```bash
# Add to crontab (crontab -e)
0 * * * * curl http://localhost:5000/cleanup
```

## 🐛 Troubleshooting

### Common Issues

1. **"No module named 'PIL'"**
   ```bash
   pip install Pillow
   ```

2. **Permission denied errors**
   - Ensure the application has write permissions for `uploads/` and `outputs/` directories

3. **File not found errors**
   - Check if cleanup removed files too quickly
   - Increase cleanup interval for high-traffic scenarios

### Debug Mode
Enable debug mode for development:
```python
app.run(debug=True)
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 🙏 Acknowledgments

- **Flask** - Web framework
- **Pillow** - Image processing library
- **ReportLab** - PDF generation
- **python-docx** - Word document creation
- **SVGWrite** - SVG file generation
- **Font Awesome** - Icons
