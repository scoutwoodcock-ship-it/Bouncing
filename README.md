// Declare the shapes list at the top
ArrayList<MyShape> shapes;

void setup() {
  size(800, 600);
  shapes = new ArrayList<MyShape>();
  
  // Add one default shape to begin with
  shapes.add(new MyShape());
}

void draw() {
  background(240);
  
  for (MyShape s : shapes) {
    s.update();
    s.display();
  }
}

void mousePressed() {
  shapes.add(new MyShape(mouseX, mouseY));
}

// Define the shape class
class MyShape {
  float x, y;
  float dx, dy;
  float radius;

  // Default constructor (random position)
  MyShape() {
    x = random(width);
    y = random(height);
    dx = random(-3, 3);
    dy = random(-3, 3);
    radius = random(15, 30);
  }

  // Constructor with custom location
  MyShape(float x_, float y_) {
    x = x_;
    y = y_;
    dx = random(-3, 3);
    dy = random(-3, 3);
    radius = random(15, 30);
  }

  // Move and bounce
  void update() {
    x += dx;
    y += dy;

    if (x < radius || x > width - radius) {
      dx *= -1;
      x = constrain(x, radius, width - radius);
    }

    if (y < radius || y > height - radius) {
      dy *= -1;
      y = constrain(y, radius, height - radius);
    }
  }

  // Draw the shape
  void display() {
    fill(100, 150, 255);
    stroke(30);
    ellipse(x, y, radius * 2, radius * 2);
  }
}
