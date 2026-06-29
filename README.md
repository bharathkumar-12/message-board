# Message Board

A lightweight, production-ready Django message board application for creating and displaying posts in a simple, efficient interface.

## 🚀 Features

- **Post Management**: Create, view, and manage text-based posts
- **Admin Interface**: Full Django admin integration for content moderation
- **Responsive Design**: Bootstrap 4-powered responsive UI
- **Database Persistence**: SQLite database for reliable data storage
- **Production Ready**: Configured for Heroku deployment with Gunicorn

## 🏗️ Architecture

### Technology Stack

- **Backend Framework**: Django 3.0
- **Database**: SQLite3
- **WSGI Server**: Gunicorn 19.9.0
- **Frontend**: HTML5, Bootstrap 4
- **Python**: 3.8+
- **Package Management**: Pipenv

### Project Structure

```
message-board/
├── mb/                         # Django project configuration
│   ├── settings.py            # Application settings & configuration
│   ├── urls.py                # Root URL routing
│   ├── wsgi.py                # WSGI application entry point
│   └── asgi.py                # ASGI application entry point
│
├── posts/                      # Posts application module
│   ├── models.py              # Post data model
│   ├── views.py               # View controllers (ListView)
│   ├── urls.py                # App-specific URL routing
│   ├── admin.py               # Admin panel configuration
│   └── migrations/            # Database migrations
│
├── templates/                  # HTML templates
│   └── home.html              # Homepage template with post list
│
├── db.sqlite3                 # SQLite database
├── manage.py                  # Django management script
├── Pipfile                    # Pipenv dependencies
├── Procfile                   # Heroku deployment config
└── README.md                  # Project documentation
```

### Application Flow

```
User Request → URL Router (urls.py) → View Controller (views.py)
                                            ↓
                                       Model (models.py)
                                            ↓
                                       Database (SQLite)
                                            ↓
                                     Template (home.html)
                                            ↓
                                      Response (HTML)
```

## 📋 Database Schema

### Post Model

| Field | Type      | Description                     |
| ----- | --------- | ------------------------------- |
| id    | AutoField | Primary key (auto-generated)    |
| text  | TextField | Post content (unlimited length) |

**Model Methods:**

- `__str__()`: Returns first 50 characters of post text

## 🔧 Installation & Setup

### Prerequisites

- Python 3.8 or higher
- Pipenv (recommended) or pip

### Local Development

1. **Clone the repository**

   ```bash
   git clone <repository-url>
   cd message-board
   ```

2. **Install dependencies**

   ```bash
   # Using Pipenv (recommended)
   pipenv install
   pipenv shell

   # Or using pip
   pip install -r requirements.txt
   ```

3. **Run database migrations**

   ```bash
   python manage.py migrate
   ```

4. **Create a superuser** (for admin access)

   ```bash
   python manage.py createsuperuser
   ```

5. **Start the development server**

   ```bash
   python manage.py runserver
   ```

6. **Access the application**
   - Homepage: http://localhost:8000
   - Admin Panel: http://localhost:8000/admin

## 🎯 Usage

### Creating Posts

Posts can be created through the Django admin interface:

1. Navigate to http://localhost:8000/admin
2. Log in with superuser credentials
3. Click on "Posts" → "Add Post"
4. Enter post text and save

### Viewing Posts

All posts are displayed on the homepage at the root URL (`/`), rendered in a Bootstrap-styled list format.

## 🚢 Deployment

### Heroku Deployment

The application is configured for Heroku deployment with included `Procfile`:

1. **Install Heroku CLI**

   ```bash
   brew install heroku/brew/heroku
   ```

2. **Login to Heroku**

   ```bash
   heroku login
   ```

3. **Create Heroku app**

   ```bash
   heroku create your-app-name
   ```

4. **Deploy**

   ```bash
   git push heroku main
   ```

5. **Run migrations on Heroku**

   ```bash
   heroku run python manage.py migrate
   heroku run python manage.py createsuperuser
   ```

6. **Open application**
   ```bash
   heroku open
   ```

### Production Considerations

⚠️ **Before deploying to production:**

1. **Update SECRET_KEY**: Generate a new secret key and store in environment variables

   ```python
   SECRET_KEY = os.environ.get('SECRET_KEY')
   ```

2. **Set DEBUG to False**

   ```python
   DEBUG = False
   ```

3. **Configure ALLOWED_HOSTS**

   ```python
   ALLOWED_HOSTS = ['your-domain.com', 'www.your-domain.com']
   ```

4. **Use PostgreSQL**: Replace SQLite with PostgreSQL for production

   ```bash
   heroku addons:create heroku-postgresql:hobby-dev
   ```

5. **Configure static files**: Set up WhiteNoise or S3 for static file serving

## 🛠️ Development

### Key Components

#### Views (Class-Based Views)

- **Homepageview**: ListView that queries all posts and renders them on the homepage

#### URL Configuration

- Root URL (`/`) → Homepage with post listing
- `/admin/` → Django admin interface

#### Templates

- Uses Django template language with Bootstrap 4 CDN
- Context variable: `all_posts_list` contains all Post objects

### Adding Features

#### Example: Adding Post Titles

1. **Update Model**

   ```python
   class Post(models.Model):
       title = models.CharField(max_length=200)
       text = models.TextField()
       created_at = models.DateTimeField(auto_now_add=True)
   ```

2. **Create Migration**

   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

3. **Update Template**
   ```html
   {% for post in all_posts_list %}
   <h3>{{ post.title }}</h3>
   <p>{{ post.text }}</p>
   {% endfor %}
   ```

## 🧪 Testing

Run tests with:

```bash
python manage.py test
```

## 📝 Code Style

The project follows Django best practices:

- Class-based views for scalability
- Proper app separation (posts app)
- Template inheritance structure
- Admin interface integration

## 🔐 Security Notes

- SECRET_KEY is hardcoded (change for production)
- DEBUG mode is enabled (disable for production)
- ALLOWED_HOSTS set to `['*']` (restrict for production)
- No HTTPS enforcement (configure for production)

## 📦 Dependencies

- **Django 3.0**: Web framework
- **Gunicorn 19.9.0**: WSGI HTTP server for production

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 🐛 Known Issues

- Model naming convention uses lowercase 'post' (should be 'Post' per PEP 8)
- No pagination implemented for post listing
- No user authentication for post creation
- Limited error handling and validation

## 🗺️ Roadmap

- [ ] Add pagination for post listing
- [ ] Implement user authentication and authorization
- [ ] Add rich text editor for post content
- [ ] Include timestamps (created_at, updated_at)
- [ ] Add comment functionality
- [ ] Implement post search and filtering
- [ ] Add REST API endpoints (Django REST Framework)
- [ ] Include unit and integration tests
- [ ] Add post categories/tags
- [ ] Implement like/voting system

## 📞 Support

For issues, questions, or contributions, please open an issue in the repository.

---

**Built with Django 🎸 | Powered by Python 🐍**

---

## Maintenance

Last maintenance update: <!--LAST_UPDATED-->2026-06-29<!--/LAST_UPDATED-->
