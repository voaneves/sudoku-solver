# sudoku-solver

> Sudoku solver in Python that models Sudoku as a **linear (integer) programming** problem and solves it with [PuLP](https://github.com/coin-or/pulp). Supports classic and diagonal Sudoku.

**Keywords:** sudoku solver python, sudoku linear programming, integer programming, PuLP, constraint satisfaction, diagonal sudoku, Jupyter notebook.

## What it does

`sudoku_solver.ipynb` solves any 9x9 board given as a list of lists (`0` = empty cell) and prints the solved grid. It handles the standard rules and the "diagonal Sudoku" variant.

## How it works: Sudoku as a linear problem

- **Decision variables:** 9x9x9 binary variables `x[row][col][value]`; `1` means the cell holds that value.
- **Objective:** none (a constant `0`). Only a feasible solution is needed, not an optimal one.
- **Constraints:**
  1. each cell has exactly one value from 1 to 9;
  2. each row contains every value from 1 to 9 once;
  3. each column contains every value from 1 to 9 once;
  4. each 3x3 box contains every value from 1 to 9 once;
  5. (optional, `diagonal=True`) both main diagonals contain every value once;
  6. the pre-filled cells of the input board are fixed as constraints.
- PuLP's default solver (CBC) finds a feasible assignment; if the status is `Optimal`, the solution is extracted and printed.

## Libraries

- [`pulp`](https://pypi.org/project/PuLP/), the only import (`import pulp as plp`). The notebook installs it with `%pip install pulp`.

## Running the notebook

```bash
git clone https://github.com/voaneves/sudoku-solver.git
cd sudoku-solver
pip install pulp jupyter
jupyter notebook sudoku_solver.ipynb
```

Run all cells. Section 6 contains two examples (a normal and a diagonal board). To solve your own board:

```python
my_board = [[0]*9 for _ in range(9)]  # fill known values, 0 = empty
solve_sudoku(input_sudoku=my_board, diagonal=False)
```

## Limitations

- 9x9 boards only.
- If the puzzle has no solution, only the solver status is printed.
- The "Random board creator" section of the notebook is still an unfinished placeholder.

## Em português

Resolvedor de Sudoku em Python que trata o jogo como um problema de programação linear inteira, com variáveis binárias (linha, coluna, valor) e restrições de célula, linha, coluna, bloco 3x3, diagonais (opcional) e valores pré-preenchidos, resolvido com a biblioteca PuLP. Para rodar: `pip install pulp jupyter` e abra `sudoku_solver.ipynb`; use `solve_sudoku(tabuleiro, diagonal=False)`, com `0` nas células vazias.

## License

MIT, see [LICENSE](LICENSE).