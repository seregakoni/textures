# textures
import matplotlib.pyplot as plt
import numpy as np
import random
import matplotlib.patches as patches

def generate_texture(ax, texture_type="swirl"):
    """Generate a stretchy candy-like texture inside the shape."""
    if texture_type == "swirl":
        theta = np.linspace(0, 4 * np.pi, 200)
        r = np.linspace(0.1, 1, 200)
        x = r * np.cos(theta)
        y = r * np.sin(theta)
        ax.plot(x, y, color="white", linewidth=2)
    elif texture_type == "stripes":
        for i in range(-5, 6):
            ax.add_patch(patches.Rectangle((-1, i * 0.2), 2, 0.1, color="white", alpha=0.6))
    elif texture_type == "marbled":
        for _ in range(10):
            x = np.random.uniform(-1, 1, 100)
            y = np.random.uniform(-1, 1, 100)
            ax.scatter(x, y, color="white", alpha=0.3, s=5)

def draw_candy(shape="circle", texture="swirl"):
    fig, ax = plt.subplots()
    ax.set_aspect('equal')
    ax.set_xticks([])
    ax.set_yticks([])
    ax.set_xlim(-1.5, 1.5)
    ax.set_ylim(-1.5, 1.5)
    
    color = random.choice(["red", "blue", "green", "yellow", "pink", "orange", "purple"])
    
    if shape == "circle":
        circle = plt.Circle((0, 0), 1, color=color)
        ax.add_patch(circle)
    elif shape == "square":
        square = plt.Rectangle((-1, -1), 2, 2, color=color)
        ax.add_patch(square)
    elif shape == "heart":
        t = np.linspace(0, 2 * np.pi, 100)
        x = 0.5 * np.sin(t) ** 3
        y = 0.5 * (0.8125 * np.cos(t) - 0.3125 * np.cos(2*t) - 0.125 * np.cos(3*t) - 0.0625 * np.cos(4*t))
        ax.fill(x, y, color=color)
    elif shape == "star":
        theta = np.linspace(0, 2*np.pi, 10)
        r = np.array([1, 0.4, 0.8, 0.4, 0.8, 0.4, 0.8, 0.4, 1, 0.4])
        x = r * np.cos(theta)
        y = r * np.sin(theta)
        ax.fill(x, y, color=color)
    else:
        print("Unknown shape! Available: circle, square, heart, star")
        return
    
    generate_texture(ax, texture)
    plt.title(f"Candy Shape: {shape.capitalize()} with {texture.capitalize()} Texture")
    plt.show()

# Example usage
draw_candy("heart", "swirl")
