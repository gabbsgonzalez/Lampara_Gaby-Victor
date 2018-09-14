# Lampara_Gaby-Victor
import peasy.*; 

Pendulo pendulo1;
Pendulo pendulo2;
Pendulo pendulo3;

Pendulo pendulo4;
Pendulo pendulo5;
Pendulo pendulo6;

PGraphics canvas;
PeasyCam cam;

void setup() {
  size(900, 900,P3D);
  //cx = width/2;
  //cy = 200;
  canvas = createGraphics(width, height);
  canvas.beginDraw();
  canvas.background(255);
  canvas.endDraw();
  cam = new PeasyCam(this, height);
  colorMode(HSB);
  
  pendulo1 = new Pendulo();
  pendulo2 = new Pendulo();
  pendulo3 = new Pendulo();
  
  pendulo4 = new Pendulo();
  pendulo5 = new Pendulo();
  pendulo6 = new Pendulo();
}

void draw() {
  background(0);
  
  pendulo1.Draw();
  
  pushMatrix();
  
  pendulo2.Draw();
  rotateX(radians(-120));
  
// OTRA CLASE
class Pendulo {
  float r1 = 200;
  float r2 = 200;
  float m1 = 40;
  float m2 = 40;
  float a1 = PI/random(1, 3);
  float a2 = PI/random(1.5, 3);
  float a1_v = 0;
  float a2_v = 0;
  float g = 1;

  float px2 = -1;
  float py2 = -1;

  ArrayList<PVector> points = new ArrayList<PVector>();

  float x = 0;
  float y = 0;
  float z = 0;

  float hu;
  //más variables 
  Pendulo() {
  }

  Pendulo(float r1, float r2) {
    this.r1 = r1;
    this.r2 = r2;
  }
  void Draw() {
    float num1, num2, num3, num4, den, a1_a, a2_a, x1, x2, y1, y2;
    num1 = -g * (2 * m1 + m2) * sin(a1);
    num2 = -m2 * g * sin(a1-2*a2);
    num3 = -2*sin(a1-a2)*m2;
    num4 = a2_v*a2_v*r2+a1_v*a1_v*r1*cos(a1-a2);
    den = r1 * (2*m1+m2-m2*cos(2*a1-2*a2));
    a1_a = (num1 + num2 + num3*num4) / den;

    num1 = 2 * sin(a1-a2);
    num2 = (a1_v*a1_v*r1*(m1+m2));
    num3 = g * (m1 + m2) * cos(a1);
    num4 = a2_v*a2_v*r2*m2*cos(a1-a2);
    den = r2 * (2*m1+m2-m2*cos(2*a1-2*a2));
    a2_a = (num1*(num2+num3+num4)) / den;
    x1 = r1 * sin(a1);
    y1 = r1 * cos(a1);

    x2 = x1 + r2 * sin(a2);
    y2 = y1 + r2 * cos(a2);
    a1_v += a1_a;
    a2_v += a2_a;
    a1 += a1_v;
    a2 += a2_v;
    points.add(new PVector(x2, y2, x1));

    px2 = x2;
    py2 = y2;

    for (int i=0; i<points.size()-1; i++) {
      line(points.get(i).x, points.get(i).y, points.get(i).z, points.get(i+1).x, points.get(i+1).y, points.get(i+1).z);

      stroke(hu, 255, 255);

      hu+=0.1;

