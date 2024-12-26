# Email Marketing Platform

A comprehensive email marketing platform with multiple backend implementations (Laravel & NestJS) and a modern React dashboard. This platform allows users to create, manage, and send email campaigns to subscribers with advanced features like templates, mailing lists, and analytics.

## 🚀 Features

### Core Features
- **Multi-Backend Architecture**: Choose between Laravel and NestJS backends
- **Modern React Dashboard**: Professional UI built with TypeScript and Tailwind CSS
- **Campaign Management**: Create, edit, schedule, and send email campaigns
- **Subscriber Management**: Import, organize, and manage subscribers with tags and custom fields
- **Mailing Lists**: Organize subscribers into targeted lists
- **Template System**: Create reusable email templates (public and private)
- **Email Integration**: SendGrid integration for reliable email delivery
- **Queue System**: Background processing for bulk email sending
- **Analytics**: Track open rates, click rates, and campaign performance
- **Authentication**: Secure JWT-based authentication

### Advanced Features
- **Package Integration**: Can be integrated as a package in existing projects
- **API-First Design**: RESTful APIs for all functionality
- **Real-time Updates**: Live campaign status and progress tracking
- **Responsive Design**: Mobile-friendly interface
- **Search & Filtering**: Advanced search and filtering capabilities
- **Bulk Operations**: Import subscribers via CSV, bulk email sending
- **Error Handling**: Comprehensive error handling and logging

## 📁 Project Structure

```
email-marketing-platform/
├── laravel-email-marketing/     # Laravel backend
├── nestjs-email-marketing/      # NestJS backend  
├── react-marketing-dashboard/   # React frontend
├── PROJECT_SPECIFICATION.md     # Detailed specifications
├── DEVELOPMENT_TIMELINE.md      # Development timeline
└── README.md                   # This file
```

## 🛠️ Tech Stack

### Laravel Backend
- **Framework**: Laravel 11
- **Authentication**: Laravel Sanctum
- **Database**: SQLite (configurable to MySQL/PostgreSQL)
- **Queue**: Database queue driver
- **Email**: SendGrid integration
- **Validation**: Laravel Form Requests
- **API**: RESTful API with JSON responses

### NestJS Backend
- **Framework**: NestJS with TypeScript
- **Authentication**: JWT with Passport.js
- **Database**: In-memory (demo) / configurable to any database
- **Queue**: Custom queue service with Bull (Redis-based)
- **Email**: SendGrid integration
- **Validation**: Class-validator decorators
- **API**: RESTful API with decorators

### React Frontend
- **Framework**: React 18 with TypeScript
- **Styling**: Tailwind CSS
- **Routing**: React Router DOM
- **State Management**: React Context API
- **HTTP Client**: Axios
- **Icons**: Lucide React
- **Build Tool**: Create React App

## 🚀 Quick Start

### Prerequisites
- Node.js 16+ and npm
- PHP 8.1+ and Composer (for Laravel)
- Git

### 1. Clone and Setup

```bash
# Clone the repository
git clone <repository-url>
cd email-marketing-platform

# Setup Laravel Backend
cd laravel-email-marketing
composer install
cp .env.example .env
php artisan key:generate
php artisan migrate
php artisan serve # Runs on http://localhost:8000

# Setup NestJS Backend (in new terminal)
cd ../nestjs-email-marketing
npm install
npm run start:dev # Runs on http://localhost:3001

# Setup React Frontend (in new terminal)
cd ../react-marketing-dashboard
npm install
npm start # Runs on http://localhost:3000
```

### 2. Configure Email Service

#### For Laravel (.env):
```env
SENDGRID_API_KEY=your_sendgrid_api_key_here
MAIL_FROM_ADDRESS="noreply@yourdomain.com"
MAIL_FROM_NAME="Your App Name"
```

#### For NestJS (.env):
```env
SENDGRID_API_KEY=your_sendgrid_api_key_here
MAIL_FROM_ADDRESS=noreply@yourdomain.com
MAIL_FROM_NAME=Your App Name
```

### 3. Access the Application

- **React Dashboard**: http://localhost:3000
- **Laravel API**: http://localhost:8000/api
- **NestJS API**: http://localhost:3001

## 📚 API Documentation

### Authentication Endpoints
```
POST /auth/register - Register new user
POST /auth/login    - Login user
POST /auth/logout   - Logout user
```

### Campaign Endpoints
```
GET    /campaigns           - List campaigns
POST   /campaigns           - Create campaign
GET    /campaigns/{id}      - Get campaign
PUT    /campaigns/{id}      - Update campaign
DELETE /campaigns/{id}      - Delete campaign
POST   /campaigns/{id}/send - Send campaign
GET    /campaigns/{id}/stats - Get campaign statistics
```

### Subscriber Endpoints
```
GET    /subscribers              - List subscribers (with filtering)
POST   /subscribers              - Create subscriber
GET    /subscribers/{id}         - Get subscriber
PUT    /subscribers/{id}         - Update subscriber
DELETE /subscribers/{id}         - Delete subscriber
POST   /subscribers/{id}/unsubscribe - Unsubscribe
POST   /subscribers/import       - Import subscribers from CSV
```

### Mailing List Endpoints
```
GET    /mailing-lists     - List mailing lists
POST   /mailing-lists     - Create mailing list
GET    /mailing-lists/{id} - Get mailing list
PUT    /mailing-lists/{id} - Update mailing list
DELETE /mailing-lists/{id} - Delete mailing list
```

### Template Endpoints
```
GET    /templates              - List templates
POST   /templates              - Create template
GET    /templates/{id}         - Get template
PUT    /templates/{id}         - Update template
DELETE /templates/{id}         - Delete template
POST   /templates/{id}/duplicate - Duplicate template
GET    /templates/public       - Get public templates
```

## 🔧 Configuration

### Backend Switching
The React frontend can switch between Laravel and NestJS backends:

```typescript
// In React app
apiService.switchBackend('laravel'); // or 'nestjs'
```

### Environment Variables

#### Laravel (.env)
```env
APP_NAME="Email Marketing Platform"
DB_CONNECTION=sqlite
QUEUE_CONNECTION=database
SENDGRID_API_KEY=your_key_here
SANCTUM_STATEFUL_DOMAINS=localhost:3000,127.0.0.1:3000
```

#### NestJS (.env)
```env
PORT=3001
JWT_SECRET=your_jwt_secret_here
SENDGRID_API_KEY=your_key_here
MAIL_FROM_ADDRESS=noreply@yourdomain.com
```

#### React (.env)
```env
REACT_APP_API_URL=http://localhost:8000/api  # Laravel
# OR
REACT_APP_API_URL=http://localhost:3001      # NestJS
```

## 📦 Using as a Package

### Laravel Package Integration

1. **Install via Composer** (when published):
```bash
composer require your-org/email-marketing-platform
```

2. **Publish Configuration**:
```bash
php artisan vendor:publish --provider="EmailMarketing\ServiceProvider"
```

3. **Run Migrations**:
```bash
php artisan migrate
```

4. **Use in Your App**:
```php
use EmailMarketing\Services\EmailService;
use EmailMarketing\Models\Campaign;

// Create campaign
$campaign = Campaign::create([
    'name' => 'Welcome Series',
    'subject' => 'Welcome!',
    'content' => '<h1>Welcome to our platform!</h1>'
]);

// Send campaign
$emailService = new EmailService();
$campaign->send();
```

### NestJS Package Integration

1. **Install via NPM** (when published):
```bash
npm install @your-org/email-marketing-platform
```

2. **Import Module**:
```typescript
import { EmailMarketingModule } from '@your-org/email-marketing-platform';

@Module({
  imports: [EmailMarketingModule.forRoot({
    sendgridApiKey: 'your-key',
    fromEmail: 'noreply@yourdomain.com'
  })],
})
export class AppModule {}
```

3. **Use Services**:
```typescript
import { CampaignsService } from '@your-org/email-marketing-platform';

@Injectable()
export class MyService {
  constructor(private campaignsService: CampaignsService) {}
  
  async createCampaign() {
    return this.campaignsService.create(userId, {
      name: 'Welcome Series',
      subject: 'Welcome!',
      content: '<h1>Welcome!</h1>'
    });
  }
}
```

## 🧪 Testing

### Laravel Testing
```bash
cd laravel-email-marketing
php artisan test
```

### NestJS Testing
```bash
cd nestjs-email-marketing
npm run test
npm run test:e2e
```

### React Testing
```bash
cd react-marketing-dashboard
npm test
```

## 🚀 Deployment

### Laravel Deployment
1. Configure production environment
2. Set up database (MySQL/PostgreSQL)
3. Configure Redis for queues
4. Set up queue workers: `php artisan queue:work`
5. Configure web server (Nginx/Apache)

### NestJS Deployment
1. Build the application: `npm run build`
2. Set up Redis for Bull queues
3. Configure environment variables
4. Deploy with PM2 or Docker

### React Deployment
1. Build the application: `npm run build`
2. Deploy to CDN or static hosting
3. Configure API URLs for production

## 📈 Performance Considerations

- **Queue Processing**: Use Redis for production queue processing
- **Database Optimization**: Add indexes for frequently queried fields
- **Caching**: Implement Redis caching for frequently accessed data
- **Email Rate Limiting**: Configure SendGrid rate limits
- **CDN**: Use CDN for React frontend assets

## 🔒 Security Features

- **JWT Authentication**: Secure token-based authentication
- **Input Validation**: Comprehensive input validation on all endpoints
- **CORS Configuration**: Proper CORS setup for cross-origin requests
- **SQL Injection Protection**: ORM-based queries prevent SQL injection
- **XSS Protection**: Input sanitization and output encoding
- **Rate Limiting**: API rate limiting to prevent abuse

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `git commit -m 'Add amazing feature'`
4. Push to the branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

For support, email support@yourdomain.com or create an issue in the repository.

## 🗺️ Roadmap

- [ ] Advanced Analytics Dashboard
- [ ] A/B Testing for Campaigns
- [ ] Webhook Integration
- [ ] Multi-language Support
- [ ] Advanced Segmentation
- [ ] Drag-and-Drop Email Builder
- [ ] Social Media Integration
- [ ] Advanced Automation Workflows

---

**Built with ❤️ by [Your Name]**