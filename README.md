# 🗻 FDF - Fil de Fer (Wireframe)

[![42 School Project](https://img.shields.io/badge/42-Project-000000?style=flat&logo=42&logoColor=white)](https://42.fr)
[![Language](https://img.shields.io/badge/Language-C-blue.svg)](https://en.wikipedia.org/wiki/C_(programming_language))
[![Graphics](https://img.shields.io/badge/Graphics-MLX42-red.svg)](https://github.com/codam-coding-college/MLX42)

A 3D wireframe renderer that transforms 2D heightmaps into interactive 3D visualizations. Built as part of the 42 curriculum to explore fundamental computer graphics concepts including 3D transformations, quaternion rotations, and rasterization algorithms.

![FDF Demo](https://via.placeholder.com/800x400/0a0a0a/ffffff?text=3D+Wireframe+Visualization)

## ✨ Features

### 🎮 Interactive Controls
- **Real-time 3D rotation** using quaternion mathematics
- **Smooth zoom and pan** functionality
- **Dynamic height scaling** for terrain visualization
- **Keyboard controls** for intuitive navigation

### 🔧 Technical Highlights
- **Quaternion-based rotations** for smooth, gimbal-lock-free transformations
- **Bresenham's line algorithm** for efficient wireframe rendering
- **Custom MLX42 graphics engine** integration
- **Memory-efficient 2D array management**
- **Automatic viewport centering and scaling**

### 📊 File Format Support
- **FDF heightmaps** - Space-separated integer matrices
- **Color support** - Hexadecimal color values (0xRRGGBB)
- **Variable dimensions** - Automatic detection of map size

## 🚀 Quick Start

### Prerequisites
- **macOS** (MLX42 dependency)
- **Homebrew** package manager
- **GLFW** graphics library

```bash
# Install dependencies
brew install glfw
```

### Installation & Usage

```bash
# Clone the repository
git clone "git@github.com:Codam-Max-Valk/fdf.git"
cd fdf

# Build the project
make

# Run with a heightmap file
./fdf test_maps/42.fdf
```

## 🎯 Controls

| Key | Action |
|-----|--------|
| **WASD** | Pan the view |
| **Q/E** | Rotate around Z-axis |
| **Keypad 8/5** | Rotate around X-axis |
| **Keypad 4/6** | Rotate around Y-axis |
| **+/-** | Zoom in/out |
| **I/K** | Scale height |
| **R** | Reset to default view |
| **F** | Reset to flat view |
| **ESC** | Exit |

## 🗺️ Map Format

FDF files are simple text files containing space-separated integers representing heights:

```
0  0  0  0  0  0  0  0  0
0  0  0  0  0  0  0  0  0
0  0 10 10  0  0 10 10  0
0  0 10 10  0  0 10 10  0
0  0  0  0  0  0  0  0  0
```

### With Colors
```
0  0  0  0  0
0 10,0xFF0000 10,0xFF0000  0  0
0 10,0x00FF00 10,0x00FF00  0  0
0  0  0  0  0
```

## 🏗️ Architecture

### Core Components

```
├── src/
│   ├── main.c              # Entry point and argument handling
│   ├── init_fdf.c          # MLX42 initialization and setup
│   ├── file_utils.c        # Map file parsing and validation
│   ├── generate_image.c    # Wireframe rendering engine
│   ├── image_utils.c       # Line drawing algorithms
│   ├── rotate_points.c     # Quaternion rotation mathematics
│   ├── key_moves.c         # Input handling and transformations
│   └── fdf_utils.c         # Utility functions
├── libft/                  # Custom C library
├── MLX42/                  # Graphics library
└── test_maps/              # Sample heightmap files
```

### Key Data Structures

```c
typedef struct s_point3d {
    int32_t  x, y;      // 2D screen coordinates
    double   z;         // Height value
    int32_t  col;       // Color information
} t_point3d;

typedef struct s_quaternion {
    double w, x, y, z;  // Quaternion components
} t_quaternion;

typedef struct s_fdf {
    mlx_t        *mlx;     // MLX42 instance
    mlx_image_t  *image;   // Render target
    t_point3d    **map;    // 2D heightmap array
    t_frame      *frame;   // Current transformation state
    // ... other components
} t_fdf;
```

## 🧮 Mathematical Concepts

### Quaternion Rotations
The project implements quaternion-based 3D rotations to avoid gimbal lock:

```c
// Convert axis-angle to quaternion
t_quaternion quaternion_axis_angle(double angle, double x, double y, double z) {
    double s = sin(angle / 2.0);
    double c = cos(angle / 2.0);
    return (t_quaternion){c, x * s, y * s, z * s};
}
```

### Line Rasterization
Uses Bresenham's algorithm for efficient line drawing:

```c
// Optimized line drawing with error diffusion
while (true) {
    put_pixel(x, y, color);
    if (x == end_x && y == end_y) break;
    
    e2 = 2 * err;
    if (e2 > -dy) { err -= dy; x += sx; }
    if (e2 < dx)  { err += dx; y += sy; }
}
```

## 🎨 Example Visualizations

The project includes various test maps demonstrating different features:

- **`42.fdf`** - The iconic 42 logo in 3D
- **`mars.fdf`** - Martian terrain heightmap
- **`julia.fdf`** - Julia set fractal
- **`pyramide.fdf`** - Pyramid structure
- **Color maps** - Maps with embedded color information

## 🛠️ Technical Deep Dive

### Memory Management
- Dynamic 2D array allocation for variable map sizes
- Proper cleanup of all MLX42 resources
- Error handling with appropriate exit codes

### Performance Optimizations
- Efficient quaternion multiplication
- Minimal memory allocations during rendering
- Optimized line drawing with integer arithmetic

### Graphics Pipeline
1. **Parse** heightmap file into 2D point array
2. **Transform** points using quaternion rotations
3. **Project** 3D coordinates to 2D screen space
4. **Rasterize** wireframe using line drawing
5. **Display** result with MLX42

## 🎓 Learning Outcomes

This project reinforces fundamental computer graphics concepts:

- **3D Mathematics**: Quaternions, matrix transformations, coordinate systems
- **Rasterization**: Line drawing algorithms, pixel manipulation
- **Memory Management**: Dynamic allocation, resource cleanup
- **Event Handling**: Real-time user input processing
- **Graphics APIs**: Working with MLX42/OpenGL concepts

## 📝 42 Project Requirements

- ✅ Read and parse FDF heightmap files
- ✅ Render wireframe representation
- ✅ Implement interactive controls
- ✅ Handle various map sizes and formats
- ✅ Proper error handling and memory management
- ✅ Smooth transformations and user experience

## 🤝 Contributing

This is an educational project, but contributions are welcome:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## 📄 License

This project is part of the 42 School curriculum. Feel free to reference for learning purposes.

---

**Built with ❤️ by [mvalk](https://github.com/Max-Valk) at [Codam Coding College](https://www.codam.nl/)**

*42 Project Score: [Your Score]/100*
