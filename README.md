# ALX Travel App

A professional Django REST API for managing travel listings, bookings, and reviews.

## 🚀 Features

- **Property Listings**: Create, read, update, and delete travel properties
- **Advanced Search**: Search and filter listings by location, price, type, and capacity
- **Booking System**: Complete booking management with status tracking
- **Review System**: Guest reviews and ratings for properties
- **User Authentication**: Secure user registration and login
- **Real-time API Documentation**: Auto-generated Swagger/OpenAPI docs
- **Asynchronous Tasks**: Email notifications and background processing with Celery
- **Production Ready**: Security best practices and environment configuration

## 🛠️ Technology Stack

- **Backend**: Django 4.2, Django REST Framework
- **Database**: MySQL
- **Task Queue**: Celery with Redis
- **Documentation**: drf-yasg (Swagger/OpenAPI)
- **Environment Management**: django-environ

## 📋 Prerequisites

- Python 3.9+
- MySQL 8.0+
- Redis (for Celery)

## ⚡ Quick Start

### 1. Clone and Setup

```bash
git clone <repository-url>
cd alx_travel_app
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
```

### 2. Environment Configuration

```bash
cp .env.dist .env
# Edit .env with your database and Redis credentials
```

### 3. Database Setup

```bash
# Create MySQL database
mysql -u root -p
CREATE DATABASE alx_travel_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
EXIT;

# Run migrations
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
```

### 4. Start Services

```bash
# Terminal 1: Django server
python manage.py runserver

# Terminal 2: Celery worker (in another terminal)
celery -A alx_travel_app worker --loglevel=info

# Terminal 3: Celery beat (for periodic tasks)
celery -A alx_travel_app beat --loglevel=info
```

## 📚 API Documentation

Once the server is running, access the interactive API documentation:

- **Swagger UI**: http://localhost:8000/swagger/
- **ReDoc**: http://localhost:8000/redoc/
- **Admin Panel**: http://localhost:8000/admin/

## 🔗 API Endpoints

### Listings
- `GET /api/v1/listings/` - List all listings
- `POST /api/v1/listings/` - Create new listing
- `GET /api/v1/listings/{id}/` - Get listing details
- `PUT/PATCH /api/v1/listings/{id}/` - Update listing
- `DELETE /api/v1/listings/{id}/` - Delete listing
- `GET /api/v1/listings/search/` - Advanced search

### Bookings
- `GET /api/v1/bookings/` - List user's bookings
- `POST /api/v1/bookings/` - Create new booking
- `POST /api/v1/bookings/{id}/confirm/` - Confirm booking (hosts only)
- `POST /api/v1/bookings/{id}/cancel/` - Cancel booking

### Reviews
- `GET /api/v1/reviews/` - List reviews
- `POST /api/v1/reviews/` - Create review
- `GET /api/v1/listings/{id}/reviews/` - Get listing reviews
- `POST /api/v1/listings/{id}/add_review/` - Add review to listing

## 🔒 Authentication

The API uses Django's token authentication. Include the token in headers:

```bash
Authorization: Token your-auth-token-here
```

Get a token by POST to `/api-auth/login/` with username/password.

## 🧪 Testing

```bash
# Run all tests
python manage.py test

# Run tests with coverage
pip install coverage
coverage run --source='.' manage.py test
coverage report
coverage html  # Generate HTML report
```

## 🚀 Deployment

### Environment Variables for Production

```bash
DEBUG=False
SECRET_KEY=your-super-secret-key
ALLOWED_HOSTS=yourdomain.com,www.yourdomain.com
DB_NAME=alx_travel_production
DB_USER=production_user
DB_PASSWORD=secure_password
REDIS_URL=redis://redis-server:6379/0
```

### Docker Deployment

```dockerfile
# Dockerfile example
FROM python:3.9
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["gunicorn", "alx_travel_app.wsgi:application", "--bind", "0.0.0.0:8000"]
```

## 🔧 Development

### Project Structure

```
alx_travel_app/
├── alx_travel_app/          # Main project settings
│   ├── settings.py          # Django settings
│   ├── urls.py              # Root URL configuration
│   ├── celery.py            # Celery configuration
│   └── wsgi.py              # WSGI application
├── listings/                # Main app
│   ├── models.py            # Database models
│   ├── serializers.py       # API serializers
│   ├── views.py             # API views
│   ├── tasks.py             # Celery tasks
│   ├── urls.py              # App URLs
│   └── admin.py             # Admin configuration
├── static/                  # Static files
├── media/                   # User uploaded files
├── logs/                    # Application logs
├── requirements.txt         # Python dependencies
├── .env.dist               # Environment template
└── manage.py               # Django management
```

### Code Style

- Follow PEP 8 guidelines
- Use meaningful variable and function names
- Add docstrings to all classes and functions
- Write tests for all new features

### Git Workflow

```bash
# Feature branch workflow
git checkout -b feature/new-feature
git add .
git commit -m "feat: add new feature description"
git push origin feature/new-feature
# Create pull request
```

### Commit Convention

- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation changes
- `style:` Code style changes
- `refactor:` Code refactoring
- `test:` Adding tests
- `chore:` Maintenance tasks

## 📊 Monitoring

### Celery Tasks

Monitor Celery tasks using Flower:

```bash
pip install flower
celery -A alx_travel_app flower
# Access http://localhost:5555
```

### Logging

Logs are stored in `logs/django.log`. Configure log levels in settings.py.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Write tests
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🆘 Support

For support and questions:
- Create an issue on GitHub
- Check the API documentation at `/swagger/`
- Review the Django documentation
