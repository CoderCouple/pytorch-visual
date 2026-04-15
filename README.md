# PyTorch Visual — Interactive Operation Visualizer

An interactive web application that brings PyTorch operations to life with step-by-step animations, color-coded tensor grids, and real-time code execution. Built for students, educators, and anyone learning deep learning fundamentals.

## Demo

<!-- Add your video/gif here -->
<!-- ![PyTorch Visual Demo](demo.mp4) -->

## Why PyTorch Visual?

Understanding tensor operations is one of the biggest hurdles when learning PyTorch. Reading documentation tells you *what* an operation does — PyTorch Visual *shows* you how it works, element by element, with smooth animations and visual breakdowns.

- **See matrix multiplication** as row-by-column dot products, computed one cell at a time
- **Watch broadcasting** stretch a smaller tensor before element-wise addition
- **Trace ReLU activation** as each value maps through the function curve
- **Step through reshaping** as elements flow from one shape to another in row-major order

## Features

### Interactive Visualizations

| Visualization | What It Shows |
|---|---|
| **Tensor Grid** | Color-coded 2D/3D grids (blue = negative, white = zero, red = positive) with hover tooltips showing exact values and indices |
| **Math Operations** | Two input grids + operator + result grid; cells highlight element-by-element as computation progresses |
| **Matrix Multiplication** | Multi-phase animation: extract row/column, multiply elements, sum products, populate result cell |
| **Reshape** | Elements flow from old shape to new shape, showing row-major ordering with grouped transitions |
| **Activation (ReLU)** | D3-rendered function curve with animated dots tracing each input to its output |

### Built-in Python Editor

Write and execute PyTorch code directly in the browser:
- Syntax-highlighted editor with line numbers
- **Shift+Enter** to run code instantly
- All tensor variables are automatically extracted and visualized
- stdout capture for `print()` statements
- Error messages displayed inline

### Animation Controls

Step through operations at your own pace:
- **Play/Pause** — auto-advance through computation steps
- **Next Step** — manually step forward one computation at a time
- **Reset** — jump back to the beginning
- **Speed Control** — 0.5x, 1x, 1.5x, 2x, 3x playback speed

### Step-by-Step Explanations

Each operation is decomposed into logical steps with:
- Numbered progression with visual highlighting of the current step
- Mathematical formula rendered with KaTeX (e.g., `C[i,j] = sum_k A[i,k] * B[k,j]`)
- Plain-text explanation of what's happening at each stage
- Syntax-highlighted PyTorch code snippet with copy button

## Supported Operations

### Tensor Basics
| Operation | Description |
|---|---|
| `torch.tensor()` | Create tensors from Python lists (1D, 2D, 3D) |
| `torch.zeros()` | Create tensors filled with zeros |
| `torch.ones()` | Create tensors filled with ones |
| `torch.rand()` | Create tensors with uniform random values in [0, 1) |
| `torch.arange()` | Create 1D tensors with evenly spaced values, optionally reshape |

### Math Operations
| Operation | Description |
|---|---|
| `torch.add()` | Element-wise addition with automatic broadcasting |

### Linear Algebra
| Operation | Description |
|---|---|
| `torch.matmul()` | Matrix multiplication with dot-product animation |

### Reshaping
| Operation | Description |
|---|---|
| `torch.reshape()` | Rearrange tensor elements into a new shape (row-major order) |

### Indexing
| Operation | Description |
|---|---|
| Indexing & Slicing | Select elements using `t[0]`, `t[:, 1]`, `t[0:2, 1:]`, etc. |

### Activations
| Operation | Description |
|---|---|
| `nn.ReLU()` | Rectified Linear Unit — zeroes out negative values, passes positives unchanged |

## Tech Stack

### Frontend
- **Framework:** [Next.js 16](https://nextjs.org/) with App Router + TypeScript
- **Styling:** [Tailwind CSS](https://tailwindcss.com/) + [shadcn/ui](https://ui.shadcn.com/) component library
- **Visualization:** [D3.js](https://d3js.org/) for color scales and SVG charts
- **Animation:** [Framer Motion](https://www.framer.com/motion/) for smooth transitions and spring physics
- **Math Rendering:** [KaTeX](https://katex.org/) for LaTeX formulas
- **Code Highlighting:** [react-syntax-highlighter](https://github.com/react-syntax-highlighter/react-syntax-highlighter) with Prism (One Dark theme)
- **Icons:** [Lucide React](https://lucide.dev/)

### Backend
- **Framework:** [FastAPI](https://fastapi.tiangolo.com/) (Python)
- **Tensor Engine:** [PyTorch](https://pytorch.org/) 2.0+
- **Validation:** Pydantic v2
- **Server:** Uvicorn (ASGI)

## Architecture

```
pytorch-visual/
├── frontend/                          # Next.js app (deployed to Vercel)
│   ├── src/
│   │   ├── app/
│   │   │   ├── layout.tsx             # Root layout with sidebar + header
│   │   │   ├── page.tsx               # Home page — category cards grid
│   │   │   └── operations/
│   │   │       └── [category]/
│   │   │           └── [operation]/
│   │   │               └── page.tsx   # Dynamic operation detail page
│   │   ├── components/
│   │   │   ├── layout/                # Sidebar, header, breadcrumb
│   │   │   ├── operations/            # Operation view, input controls,
│   │   │   │                          # animation controls, code/math/
│   │   │   │                          # explanation panels, Python editor
│   │   │   ├── visualizations/        # Tensor grid, math-op, matmul,
│   │   │   │                          # reshape, activation visualizations
│   │   │   └── ui/                    # 14 shadcn/ui components
│   │   ├── lib/
│   │   │   ├── operations-registry.ts # Operation metadata catalog
│   │   │   ├── api.ts                 # FastAPI client (execute + run-code)
│   │   │   ├── color-scales.ts        # D3 diverging color scale
│   │   │   └── animation-utils.ts     # Framer Motion presets
│   │   └── types/
│   │       └── operations.ts          # TypeScript interfaces
│   └── package.json
│
├── backend/                           # FastAPI server (local or cloud)
│   ├── main.py                        # App entry, CORS config
│   ├── requirements.txt
│   ├── routers/
│   │   └── operations.py              # API endpoints
│   └── services/
│       ├── executor.py                # Operation handlers (step-by-step)
│       ├── code_runner.py             # Safe user code execution
│       └── tensor_serializer.py       # torch.Tensor → JSON
│
└── README.md
```

## API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/operations/execute` | Execute a structured operation with step-by-step decomposition |
| `POST` | `/api/run-code` | Execute user-written Python code and extract all tensor variables |
| `GET` | `/api/operations/list` | List all available operations |
| `GET` | `/health` | Health check |

## Getting Started

### Prerequisites

- **Node.js** 18+ and npm
- **Python** 3.9+
- **PyTorch** 2.0+

### 1. Clone the repository

```bash
git clone https://github.com/CoderCouple/pytorch-visual.git
cd pytorch-visual
```

### 2. Start the backend

```bash
cd backend
python3 -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
uvicorn main:app --reload --port 8000
```

The API will be available at [http://localhost:8000](http://localhost:8000). Check [http://localhost:8000/health](http://localhost:8000/health) to verify.

### 3. Start the frontend

```bash
cd frontend
npm install
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

## How It Works

```
User writes PyTorch code          Frontend sends code to backend
in the browser editor        →    POST /api/run-code
                                       ↓
                                  Backend executes code safely
                                  in an isolated namespace
                                       ↓
                                  Extracts all tensor variables
                                  and generates step-by-step breakdown
                                       ↓
Frontend receives structured  ←   Returns: tensors, steps, stdout
response and renders                   ↓
appropriate visualization        Visualization component animates
                                  through each computation step
```

## Deployment

- **Frontend:** Deployed on [Vercel](https://vercel.com) — auto-builds from the `frontend/` directory
- **Backend:** Requires a Python runtime — deploy to [Railway](https://railway.app), [Render](https://render.com), or [Fly.io](https://fly.io), or run locally during development

## Roadmap

- [ ] **Autograd** — computation graph DAG with forward/backward flow animation
- [ ] **All Math Operations** — sub, mul, div, pow, sqrt, trig, exp, log + broadcasting visualization
- [ ] **Reductions** — sum, mean, max, min, argmax, std, cumsum with dim parameter
- [ ] **Comparisons** — eq, gt, lt, where, boolean masking
- [ ] **NN Layers** — Linear, Conv1d/2d, Embedding, Dropout with sliding window animation
- [ ] **All Activations** — Sigmoid, Tanh, LeakyReLU, GELU, Softmax, SiLU, ELU
- [ ] **Pooling** — MaxPool2d, AvgPool2d with region highlighting
- [ ] **Normalization** — BatchNorm, LayerNorm, GroupNorm with histogram distribution shifts
- [ ] **Loss Functions** — MSE, CrossEntropy, BCE, Huber with prediction vs target bars
- [ ] **Optimizers** — SGD, Adam, AdamW with gradient descent on contour plots
- [ ] **Sequence Models** — RNN, LSTM, GRU with unrolled cell animation
- [ ] **Attention** — MultiheadAttention with QKV dot products and attention weight heatmap

## License

MIT

---

Built with PyTorch, Next.js, and a lot of animations.
