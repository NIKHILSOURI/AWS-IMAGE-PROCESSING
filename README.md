# AWS Image Processing - Serverless Platform

A scalable, serverless image-processing platform implemented using Amazon Web Services (AWS). This project demonstrates a complete serverless architecture that processes images using AWS Lambda, Amazon S3, Amazon API Gateway, Amazon Rekognition, and Amazon CloudWatch.

## 🎯 Project Overview

This project implements a serverless image-processing application that can:
- **Detect labels** in images using Amazon Rekognition
- **Transform images** with operations like grayscale conversion, resizing, and thumbnail generation
- **Scale automatically** based on demand without manual server management
- **Track performance** using custom CloudWatch metrics

## 🏗️ System Architecture

### AWS Services Used

- **Amazon S3**: Two buckets for input and output storage
  - Input bucket: `dv1566-image-input-nikhil` - stores original images
  - Output bucket: `dv1566-image-output-nikhil` - stores processed images under operation-specific prefixes
- **AWS Lambda**: Core processing function `dv1566-image-processor` that handles image transformations
- **Amazon API Gateway**: HTTP API endpoint (`POST /process`) for external access
- **Amazon Rekognition**: AI-powered image analysis and label detection
- **Amazon CloudWatch**: Performance monitoring and custom metrics

### Architecture Flow

```
User Upload → API Gateway → Lambda Function → S3 Storage
                                      ↓
                              Image Processing (Pillow)
                                      ↓
                              Amazon Rekognition (Optional)
                                      ↓
                              S3 Output + CloudWatch Metrics
```

## ✨ Features

### Image Operations

1. **Labels Only**: Uses Amazon Rekognition to detect objects and scenes in images
2. **Grayscale**: Converts images to black and white
3. **Resize**: Dynamically resizes images to specified dimensions
4. **Thumbnail**: Creates thumbnail versions of images

### User Interface

- **Modern, Apple-inspired design** with elegant UI/UX
- **Drag-and-drop** file upload functionality
- **Real-time processing** with visual feedback
- **Results visualization** with processed images and detected labels
- **Performance metrics** display showing processing time

## 🚀 Getting Started

### Prerequisites

- AWS Account with appropriate permissions
- AWS Lambda function deployed (see backend setup)
- API Gateway endpoint configured

### Using the Web Interface

1. **Access the application**: The UI is deployed via GitHub Pages
2. **Upload an image**: Click or drag-and-drop an image file
3. **Select operation**: Choose from labels, grayscale, resize, or thumbnail
4. **Configure options**: Set dimensions for resize/thumbnail operations
5. **Process**: Click "Upload & Process" to start processing
6. **View results**: See the processed image, detected labels, and performance metrics

### API Usage

The backend API accepts POST requests to the `/process` endpoint:

```json
{
  "imageBase64": "<base64-encoded-image>",
  "operation": "grayscale|resize|thumbnail|labels",
  "width": 800,
  "height": 600,
  "runRekognition": true
}
```

**Response:**
```json
{
  "message": "processed_from_http",
  "operation": "grayscale",
  "output_image_bucket": "dv1566-image-output-nikhil",
  "output_image_key": "processed/grayscale/image.png",
  "processing_time_ms": 1234.56,
  "labels_count": 5,
  "labels": [
    {
      "Name": "Person",
      "Confidence": 95.5
    }
  ],
  "output_image_base64": "<base64-encoded-processed-image>"
}
```

## 📁 Project Structure

```
image-ui/
├── index.html          # Main UI application
├── README.md           # Project documentation
└── .github/
    └── workflows/
        └── deploy.yml  # GitHub Pages deployment workflow
```

## 🔧 Backend Implementation

### Lambda Function

The Lambda function (`dv1566-image-processor`) supports:

- **Multiple operations**: labels, grayscale, resize, thumbnail
- **S3 integration**: Reads from input bucket, writes to output bucket
- **Rekognition integration**: Optional label detection on processed images
- **CloudWatch metrics**: Custom metrics with operation dimensions
- **Error handling**: Comprehensive error handling and logging

### S3 Bucket Structure

**Input Bucket:**
```
dv1566-image-input-nikhil/
  └── uploads/
      └── <timestamp>.png
```

**Output Bucket:**
```
dv1566-image-output-nikhil/
  ├── processed/original/
  ├── processed/grayscale/
  ├── processed/resize/
  └── processed/thumbnail/
```

## 📊 Monitoring & Metrics

The system tracks custom CloudWatch metrics:

- **ProcessedImagesCount**: Number of successfully processed images
- **FailedImagesCount**: Number of failed processing attempts
- **ProcessingTimeMs**: Processing duration in milliseconds
- **LabelsCount**: Number of labels detected by Rekognition

All metrics include an `Operation` dimension for filtering by operation type.

## 🎨 UI Features

### Design Highlights

- **Apple-inspired aesthetic**: Clean, minimal design with smooth animations
- **Responsive layout**: Works seamlessly on desktop and mobile devices
- **Interactive elements**: Hover effects, smooth transitions, and visual feedback
- **Modern typography**: Inter font family for optimal readability
- **Color-coded status**: Visual indicators for success, error, and processing states

### User Experience

- **Drag-and-drop upload**: Intuitive file upload interface
- **Real-time status**: Live updates during processing
- **Smooth animations**: Fade-in effects and transitions
- **Error handling**: Clear error messages with visual indicators
- **Results display**: Organized presentation of processed images and labels

## 🚢 Deployment

### GitHub Pages

The application is automatically deployed to GitHub Pages using GitHub Actions:

1. **Workflow**: `.github/workflows/deploy.yml`
2. **Trigger**: On push to `main` branch
3. **Deployment**: Static files are deployed to GitHub Pages

### Manual Deployment

To deploy manually:

1. Enable GitHub Pages in repository settings
2. Select source branch (typically `main`)
3. Select root directory or `/docs` folder
4. Save settings

## 👥 Team

**Team 14** - DV1566 HT25 lp2 Introduction to Cloud Computing

- **Yalamati Nikhil Souri** - niya25@student.bth.se
- **Ajay Kumar Reddy Bindela** - ajbi25@student.bth.se
- **Shaik Mahammed Sameen** - mass25@student.bth.se

**Supervisors:**
- Emiliano Casalicchio
- Shahrooz Abghari

## 📝 License

This project is part of an academic course at Blekinge Institute of Technology (BTH).

## 🔗 Resources

- [AWS Lambda Documentation](https://docs.aws.amazon.com/lambda/)
- [Amazon S3 Documentation](https://docs.aws.amazon.com/s3/)
- [Amazon Rekognition Documentation](https://docs.aws.amazon.com/rekognition/)
- [Amazon API Gateway Documentation](https://docs.aws.amazon.com/apigateway/)
- [Amazon CloudWatch Documentation](https://docs.aws.amazon.com/cloudwatch/)

## 📈 Future Enhancements

Potential improvements for future versions:

- Additional image processing operations (blur, sharpen, rotate)
- Batch processing capabilities
- Image format conversion (JPEG, WebP, etc.)
- Advanced Rekognition features (face detection, text extraction)
- User authentication and image history
- Enhanced performance analytics dashboard
- Real-time processing status updates via WebSockets

---

**Note**: This project demonstrates serverless architecture principles and AWS service integration. The solution automatically scales with demand and requires no manual server management.
