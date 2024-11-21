## HTML

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Portfolio</title>
    <!-- Link to Bootstrap for base styling -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/css/bootstrap.min.css" integrity="sha384-TX8t27EcRE3e/ihU7zmQxVncDAy5uIKz4rEkgIXeMed4M0jlfIDPvg6uqKI2xXr2" crossorigin="anonymous">
    <!-- Custom font -->
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@500&display=swap" rel="stylesheet">
    <!-- Custom CSS -->
    <link rel="stylesheet" href="{{ url_for('static', filename='css/style.css') }}">
</head>
<body>

    <!-- Header with Navigation Links -->
    <header class="header">
        <a href="#home" class="logo">My Portfolio</a>
        <nav class="nav-links">
            <a href="#home">Home</a>
            <a href="#about">About Me</a>
            <a href="#comments">Comments</a>
            <a href="#contact">Contact</a>
        </nav>
    </header>

    <!-- Main Sections -->
    <main>
        <!-- Home Section -->
        <section id="home" class="section red-section">
            <div class="content">
                <h1 class="main-text">Mustafa Fatehi</h1>
                <p>Welcome to my portfolio! I am excited to share my work with you.</p>
            </div>
        </section>

        <!-- About Me Section -->
        <section id="about" class="section white-section">
            <div class="content">
                <h1>About Me</h1>
                <p>Hello! I'm Mustafa, a web developer experienced in Flask, Python, and front-end technologies. I create responsive, user-friendly web applications.</p>
            </div>
        </section>

        <!-- Comments Section -->
        <section id="comments" class="section comments-section">
            <div class="container">
                <h2 class="text-center">Comments</h2>

                <!-- Carousel for Comments-->
                <div id="commentCarousel" class="carousel slide" data-ride="carousel">
                    <div class="carousel-inner">
                        {% for comment in comments %}
                            <div class="carousel-item {% if loop.first %}active{% endif %}">
                                <div class="comment-box">
                                    <strong>{{ comment['NAME'] }}</strong> ({{ comment['POSITION'] }}):
                                    <p>{{ comment['COMMENT'] }}</p>
                                </div>
                            </div>
                        {% endfor %}
                    </div>
                    <a class="carousel-control-prev" href="#commentCarousel" role="button" data-slide="prev">
                        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                        <span class="sr-only">Previous</span>
                    </a>
                    <a class="carousel-control-next" href="#commentCarousel" role="button" data-slide="next">
                        <span class="carousel-control-next-icon" aria-hidden="true"></span>
                        <span class="sr-only">Next</span>
                    </a>
                </div>

                <!-- Comment Form -->
                <h3>Add a Comment</h3>
                <form action="/add_comment" method="POST" class="comment-form">
                    <div class="form-group">
                        <input type="text" name="name" class="form-control" placeholder="Your Name" required>
                    </div>
                    <div class="form-group">
                        <input type="text" name="position" class="form-control" placeholder="Your Position">
                    </div>
                    <div class="form-group">
                        <textarea name="comment" class="form-control" placeholder="Your Comment" rows="3" required></textarea>
                    </div>
                    <button type="submit" class="btn btn-primary btn-submit">Submit Comment</button>
                </form>
            </div>
        </section>

        <!-- Contact Section -->
        <section id="contact" class="contact-section">
            <div class="content">
                <h2>Contact</h2>
                <p>Phone: <a href="tel:+1234567890">+1234567890</a></p>
                <p>Email: <a href="mailto:your.email@example.com">your.email@example.com</a></p>
                <div class="social-links">
                    <a href="https://linkedin.com/in/yourusername" target="_blank">LinkedIn</a>
                    <span> | </span>
                    <a href="https://instagram.com/yourusername" target="_blank">Instagram</a>
                </div>
            </div>
        </section>
    </main>
    <!-- JavaScript for Carousel -->
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js" integrity="sha384-9/reFTGAW83EW2RDu2S0VKaIzap3H66lZH81PoYlFhbGU+6BZp6G7niu735Sk7lN" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/js/bootstrap.min.js" integrity="sha384-w1Q4orYjBQndcko6MimVbzY0tgp4pWB4lZ7lr30WKz0vr/aWKhXdBNmNb5D92v7s" crossorigin="anonymous"></script>
    <!-- JavaScript for adding a popup when comments added -->
    <script>
        document.addEventListener("DOMContentLoaded", function() {
            const form = document.querySelector('.comment-form');
            form.addEventListener('submit', function(event) {
                alert("Comment has been added!");
            });
        });
    </script>

    
</body>
</html>
```

## CSS

```css
/* Reset and Default Styles */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html, body {
  scroll-behavior: smooth;
  font-family: 'Orbitron', sans-serif;
  overflow-x: hidden;
}

body {
  display: flex;
  flex-direction: column;
}

/* Header */
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 20px;
  font-size: 1rem;
  color: #ffffff;
  background-color: #1b263b;
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 1000;
}

.logo {
  font-weight: bold;
  text-decoration: none;
  color: #ffffff;
}

.nav-links a {
  text-decoration: none;
  color: #ffffff;
  margin-left: 15px;
}

.nav-links a:hover {
  color: #a9d6e5;
}

/* Section Styling */
.section {
  min-height: 100vh;
  padding-top: 80px; /* Adjusted for fixed header */
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.content {
  max-width: 600px;
}

/* Section Background Colors */
.red-section {
  background-image: url('../images/blue_mountain.jpg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  color: #121212;
}

.white-section {
  background-color: #ffffff;
  color: #121212;
}

.contact-section {
  background-color: #f0f0f0;
  color: #333;
  padding: 40px 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  text-align: center;
}

.social-links a {
  font-weight: bold;
  color: #007bff;
  margin: 0 10px;
}

.social-links a:hover {
  text-decoration: underline;
}

/* Comments Section Styling */
.comments-section {
  background-color: #302b2b;
  padding: 40px 20px;
  text-align: center;
}

.comments-section h2, .comments-section h3 {
  margin-bottom: 20px;
  color: #ffffff;
}

/* Carousel Styling */
.carousel {
  width: 100%;
  margin-bottom: 30px;
}

.carousel-inner {
  max-width: 800px;
  margin: 0 auto;
}

.comment-box {
  background-color: #494545; /* Dark gray background */
  color: #ffffff; /* White text color */
  padding: 20px;
  border-radius: 10px;
  font-size: 1.1rem;
  text-align: left;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* Added shadow for depth */
}

/* Carousel Controls */
.carousel-control-prev, .carousel-control-next {
  color: #ffffff;
}

.carousel-control-prev-icon,
.carousel-control-next-icon {
  background-color: #ffffff; /* White icons */
  border-radius: 50%;
}

/* Comment Form Styling */
.comment-form {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px; /* Padding for better spacing */
  background-color: #383838; /* Background color for form */
  border-radius: 10px; /* Rounded corners */
}

.comment-form .form-group {
  margin-bottom: 15px;
}

.comment-form .form-control {
  font-size: 1rem;
  padding: 10px;
  background-color: #494949; /* Darker input background */
  color: #ffffff; /* White text color */
  border: none; /* Removed default border */
  border-radius: 5px; /* Rounded corners */
}

.comment-form .form-control::placeholder {
  color: #b0b0b0; /* Lighter placeholder color */
}

.btn-submit {
  background-color: #ff6b6b;
  border: none;
  color: #fff;
  padding: 10px 20px;
  font-size: 1rem;
  cursor: pointer;
  width: 100%;
  border-radius: 5px; /* Rounded corners */
  transition: background-color 0.3s; /* Smooth transition for hover */
}

.btn-submit:hover {
  background-color: #ff8566;
}
```
## Flask/Python

```python
from flask import Flask, render_template, request, redirect
from flask_sqlalchemy import SQLAlchemy

# Initialize the Flask app
app = Flask(__name__, static_folder='app/static', template_folder='app/templates')

# Configure the SQLite database
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///comments.db'
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False

# Initialize SQLAlchemy
db = SQLAlchemy(app)

# Define the Comment model
class Comment(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(80), nullable=False)
    position = db.Column(db.String(120))
    comment = db.Column(db.Text, nullable=False)

    def __repr__(self):
        return f"<Comment {self.name}>"

# Create the database tables (if not already created)
with app.app_context():
    db.create_all()

# Route for the homepage
@app.route('/')
def index():
    comments = Comment.query.all()
    return render_template('index.html', comments=[{'NAME': c.name, 'POSITION': c.position, 'COMMENT': c.comment} for c in comments])

# Route for handling the form submission
@app.route('/add_comment', methods=['POST'])
def add_comment():
    name = request.form['name']
    position = request.form['position']
    comment_text = request.form['comment']

    # Create a new comment instance and add it to the database
    new_comment = Comment(name=name, position=position, comment=comment_text)
    db.session.add(new_comment)
    db.session.commit()
    return redirect('/')

if __name__ == '__main__':
    app.run(debug=True)
```
