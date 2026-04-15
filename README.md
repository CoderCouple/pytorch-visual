# PyTorch Visual — Interactive Operation Visualizer

Interactive web app that visualizes PyTorch operations with step-by-step animations.

## Quick Start

### Backend (FastAPI + PyTorch)

```bash
cd backend
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
uvicorn main:app --reload --port 8000
```

### Frontend (Next.js)

```bash
cd frontend
npm install
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

## Phase 1 Operations

- **Tensor Basics:** `torch.tensor()`, `torch.zeros()`, `torch.rand()`
- **Math Operations:** `torch.add()` with broadcasting
- **Linear Algebra:** `torch.matmul()`
- **Reshaping:** `torch.reshape()`
- **Indexing:** Basic indexing & slicing
- **Activations:** `nn.ReLU()`

## Tech Stack

- **Frontend:** Next.js 16 + TypeScript + Tailwind CSS + shadcn/ui
- **Visualization:** D3.js + Framer Motion
- **Math:** KaTeX
- **Code:** react-syntax-highlighter
- **Backend:** FastAPI + PyTorch
