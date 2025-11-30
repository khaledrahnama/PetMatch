# PetMatch 🐾

<div align="center">
  <img src="https://raw.githubusercontent.com/khaledrahnama/PetMatch/main/assets/home.png" width="800" alt="PetMatch App Screenshots">
    <br>

   <img src="https://raw.githubusercontent.com/khaledrahnama/PetMatch/main/assets/matched.png" width="800" alt="PetMatch App Screenshots">
  <br>
  <em>From left: Home screen, Pet profiles, Matching, Chat</em>
</div>


# PetMatch 🐾

[![React Native](https://img.shields.io/badge/React_Native-0.72.0-61DAFB?style=for-the-badge&logo=react&logoColor=white)](https://reactnative.dev/)
[![Node.js](https://img.shields.io/badge/Node.js-18.x-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)](https://nodejs.org/)
[![MongoDB](https://img.shields.io/badge/MongoDB-6.0-47A248?style=for-the-badge&logo=mongodb&logoColor=white)](https://www.mongodb.com/)
[![Firebase](https://img.shields.io/badge/Firebase-FFCA28?style=for-the-badge&logo=firebase&logoColor=black)](https://firebase.google.com/)

## 📱 Overview

PetMatch is a modern mobile application that helps pet owners find perfect playmates for their furry friends. Connect with nearby pet owners, schedule playdates, and build a community of pet lovers.

## 🚀 Features

### Core Functionality
- **Pet Profile Management** - Create detailed profiles for your pets
- **Smart Matching** - AI-powered compatibility matching based on pet preferences
- **Real-time Chat** - Instant messaging with other pet owners
- **Location-based Discovery** - Find nearby pets and pet owners
- **Playdate Scheduling** - Coordinate meetups with calendar integration
- **Photo Sharing** - Share adorable pet pictures
- **Vaccination Records** - Digital health record tracking

### Social Features
- **Pet Social Feed** - Share moments and updates
- **Reviews & Ratings** - Rate playdate experiences
- **Community Events** - Discover local pet events
- **Emergency Contacts** - Quick access to nearby vet clinics

## 🛠 Technology Stack

### Frontend - Mobile Application
**React Native with TypeScript**
- **Framework**: React Native 0.72.0
- **Language**: TypeScript 4.9.5
- **State Management**: Redux Toolkit with RTK Query
- **Navigation**: React Navigation 6.x (Stack & Bottom Tabs)
- **UI Components**: 
  - React Native Paper (Material Design)
  - Custom component library
- **Animation**: React Native Reanimated 3.0
- **Forms**: React Hook Form with Yup validation

### Backend - API & Server
**Node.js with Express & TypeScript**
- **Runtime**: Node.js 18.x LTS
- **Framework**: Express.js 4.18 with TypeScript
- **API Documentation**: Swagger/OpenAPI 3.0
- **Authentication**: JWT with refresh tokens
- **Validation**: Joi with custom validators
- **Security**: Helmet, CORS, rate limiting
- **Logging**: Winston with daily file rotation

### Database & Storage
**MongoDB with Mongoose**
- **Database**: MongoDB Atlas (Cloud)
- **ODM**: Mongoose 7.0 with TypeScript support
- **Data Modeling**: 
  - Embedded documents for related data
  - Reference populations for complex relationships
- **Indexing**: Compound indexes for geospatial queries
- **Aggregation**: Pipeline for analytics and matching

### Real-time Features
**Socket.IO & Firebase**
- **WebSockets**: Socket.IO for real-time chat
- **Push Notifications**: Firebase Cloud Messaging (FCM)
- **Presence**: Online/offline status tracking

### Cloud Services & Infrastructure
**Google Cloud Platform & Firebase**
- **File Storage**: Firebase Storage for images
- **Authentication**: Firebase Auth (email/password, social login)
- **Hosting**: 
  - Frontend: Expo Application Services (EAS)
  - Backend: Google Cloud Run (Containerized)
- **CDN**: Cloudflare for static assets

### Third-party Integrations
- **Maps & Location**: Google Maps Platform
  - Places API for location search
  - Geocoding for address conversion
  - Distance Matrix for proximity calculations
- **Calendar**: Google Calendar API
- **Payments**: Stripe (premium features)
- **Email**: SendGrid for transactional emails
- **Analytics**: Google Analytics 4, Mixpanel

## 🏗 Architecture

### System Architecture
```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   Mobile App    │◄──►│   API Gateway    │◄──►│   Microservices │
│  (React Native) │    │   (Express.js)   │    │   Architecture  │
└─────────────────┘    └──────────────────┘    └─────────────────┘
         │                       │                       │
         │                       │                       │
         ▼                       ▼                       ▼
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│  Firebase Auth  │    │   MongoDB Atlas  │    │  Socket.IO WS   │
│   & Storage     │    │   (Database)     │    │  (Real-time)    │
└─────────────────┘    └──────────────────┘    └─────────────────┘
```

### Database Schema Highlights
```javascript
// User Schema
User {
  _id: ObjectId,
  email: string,
  profile: {
    name: string,
    avatar: string,
    location: GeoJSON,
    preferences: Object
  },
  pets: [PetRef],
  createdAt: Date
}

// Pet Schema
Pet {
  _id: ObjectId,
  owner: UserRef,
  name: string,
  type: 'dog' | 'cat' | 'other',
  breed: string,
  age: number,
  temperament: string[],
  photos: [string],
  vaccinationRecords: [Vaccination],
  location: GeoJSON
}

// Match Schema
Match {
  _id: ObjectId,
  pets: [PetRef],
  status: 'pending' | 'accepted' | 'rejected',
  compatibilityScore: number,
  chat: ChatRef
}
```

## 🔧 Development Setup

### Prerequisites
- Node.js 18.x or higher
- MongoDB Atlas account
- Firebase project
- Expo account
- Google Cloud Platform account

### Installation

1. **Clone the Repository**
   ```bash
   git clone https://github.com/your-org/petmatch.git
   cd petmatch
   ```

2. **Install Dependencies**
   ```bash
   # Install root dependencies
   npm install

   # Install mobile app dependencies
   cd mobile && npm install

   # Install server dependencies
   cd ../server && npm install
   ```

3. **Environment Configuration**
   ```bash
   # Mobile app (.env)
   EXPO_PUBLIC_API_URL=your_api_url
   EXPO_PUBLIC_FIREBASE_CONFIG=your_firebase_config

   # Server (.env)
   MONGODB_URI=your_mongodb_uri
   JWT_SECRET=your_jwt_secret
   FIREBASE_SERVICE_ACCOUNT=your_firebase_credentials
   ```

4. **Run Development Servers**
   ```bash
   # Start backend server
   cd server && npm run dev

   # Start mobile app (new terminal)
   cd mobile && npm start
   ```

## 📱 Build & Deployment

### Mobile App Build
```bash
# iOS build
expo build:ios

# Android build
expo build:android

# Development build
expo run:ios
expo run:android
```

### Backend Deployment
```bash
# Build Docker image
docker build -t petmatch-api .

# Deploy to GCP Cloud Run
gcloud run deploy petmatch-api --image petmatch-api
```

## 🧪 Testing

### Test Suite
- **Unit Tests**: Jest with React Native Testing Library
- **Integration Tests**: Supertest for API testing
- **E2E Tests**: Detox for mobile app testing
- **Performance**: Lighthouse CI for bundle analysis

### Running Tests
```bash
# Run all tests
npm test

# Run specific test suites
npm run test:unit
npm run test:integration
npm run test:e2e
```

## 🔒 Security Features

- **Data Encryption**: AES-256 for sensitive data
- **API Security**: JWT tokens, rate limiting, CORS
- **Input Validation**: Comprehensive sanitization
- **Privacy Controls**: Granular user privacy settings
- **Secure File Upload**: Signed URLs for cloud storage

## 📊 Performance & Monitoring

### Performance Optimization
- **Image Optimization**: WebP format, lazy loading
- **Code Splitting**: Dynamic imports for features
- **Caching**: Redis for frequent queries
- **Bundle Optimization**: Tree shaking, code splitting

### Monitoring & Analytics
- **Error Tracking**: Sentry for crash reporting
- **Performance**: Google Analytics, Custom metrics
- **Uptime Monitoring**: Pingdom, GCP Monitoring
- **Logging**: Centralized log aggregation

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

### Development Workflow
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

- 📧 Email: support@petmatch.com
- 🐛 [Bug Reports](https://github.com/your-org/petmatch/issues)
- 💬 [Community Discord](https://discord.gg/petmatch)
- 📚 [Documentation](https://docs.petmatch.com)

## 🙏 Acknowledgments

- Icons by Feather Icons and Material Design Icons
- UI components inspired by React Native Paper
- Matching algorithm based on collaborative filtering
- Special thanks to our beta testers and pet community

---

<div align="center">
  
**Made with ❤️ for pets and their humans**

[![Twitter](https://img.shields.io/badge/Twitter-@PetMatch-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/petmatch)
[![Instagram](https://img.shields.io/badge/Instagram-@PetMatch-E4405F?style=for-the-badge&logo=instagram&logoColor=white)](https://instagram.com/petmatch)

</div>
