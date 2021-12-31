# Coordinates in old image
x_ = x/scale_x
y_ = y/scale_y

# Finding neighboring points
x1 = min(int(np.floor(x_)), width-1)
y1 = min(int(np.floor(y_)), height-1)
x2 = min(int(np.ceil(x_)), width-1)
y2 = min(int(np.ceil(y_)), height-1)

Q11 = np.array(image.getpixel((x1, y1)))
Q12 = np.array(image.getpixel((x2, y1)))
Q21 = np.array(image.getpixel((x1, y2)))
Q22 = np.array(image.getpixel((x2, y2)))

# Interpolating P1 and P2
P1 = (x2-x_)*Q11 + (x_-x1)*Q12
P2 = (x2-x_)*Q21 + (x_-x1)*Q22

if x1 == x2:
  P1 = Q11
  P2 = Q22

# Interpolating P
P = (y2-y_)*P1 + (y_-y1)*P2

# Rounding P to an int tuple
P = np.round(P)
P = tuple(P.astype(int))

scaled_image.putpixel((x, y),  P)
