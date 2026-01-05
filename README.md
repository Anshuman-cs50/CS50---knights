# Knights and Knaves Puzzle Solver

A Python implementation of a logical inference engine that solves classic Knights and Knaves puzzles using propositional logic and model checking.

## Overview

This project solves Knights and Knaves puzzles, where:
- **Knights** always tell the truth
- **Knaves** always lie
- Each person is either a knight or a knave (but not both)

The solver uses propositional logic to encode puzzle constraints and employs model checking (truth table enumeration) to determine the identity of each character.

## Features

- Complete propositional logic framework with support for:
  - Symbols (propositions)
  - Logical operators: Not, And, Or, Implication, Biconditional
  - Model checking algorithm for logical entailment
- Four classic Knights and Knaves puzzles
- Clean, object-oriented design

## Project Structure

```
knights/
├── logic.py      # Logical inference engine
├── puzzle.py     # Knights and Knaves puzzle definitions
└── README.md     # This file
```

### `logic.py`
Contains the core logical inference engine:
- `Sentence`: Base class for all logical sentences
- `Symbol`: Represents atomic propositions
- `Not`, `And`, `Or`: Logical connectives
- `Implication`, `Biconditional`: Conditional operators
- `model_check()`: Checks if a knowledge base entails a query using truth table enumeration

### `puzzle.py`
Defines four Knights and Knaves puzzles:
- **Puzzle 0**: A says "I am both a knight and a knave."
- **Puzzle 1**: A says "We are both knaves." B says nothing.
- **Puzzle 2**: A says "We are the same kind." B says "We are of different kinds."
- **Puzzle 3**: A says either "I am a knight." or "I am a knave.", but you don't know which. B says "A said 'I am a knave'." B says "C is a knave." C says "A is a knight."

## Requirements

- Python 3.x (no external dependencies required)

## Usage

Run the puzzle solver:

```bash
python puzzle.py
```

The program will solve all four puzzles and display the solution for each, showing which characters are knights and which are knaves.

## Example Output

```
Puzzle 0
    A is a Knave
Puzzle 1
    A is a Knave
    B is a Knight
Puzzle 2
    A is a Knave
    B is a Knight
Puzzle 3
    A is a Knight
    B is a Knave
    C is a Knight
```

## How It Works

1. **Knowledge Encoding**: Each puzzle's statements are encoded as logical formulas using implications:
   - If a person is a Knight, their statement must be true
   - If a person is a Knave, their statement must be false

2. **Model Checking**: The `model_check()` function uses truth table enumeration to check all possible assignments of truth values to symbols. It verifies that whenever the knowledge base is true, the query (e.g., "A is a Knight") is also true.

3. **Solution**: For each puzzle, the solver checks which identity assignments (Knight/Knave) are consistent with all the given statements.

## Boolean Model

A **model** is a truth assignment mapping symbols to boolean values (`True`/`False`), represented as a Python dictionary. For example:

```python
{"A is a Knight": True, "A is a Knave": False, 
 "B is a Knight": False, "B is a Knave": True}
```

The `model_check()` function uses **truth table enumeration** to check all 2^n possible models (where n is the number of symbols). It verifies that whenever the knowledge base is `True` in a model, the query is also `True`. This recursive algorithm explores all possible truth assignments and confirms **entailment**: `KB ⊨ Q` means in every model where KB is true, Q is also true.

## Puzzle Logic

The solver encodes the fundamental rules:
- Each person is either a Knight or a Knave: `Or(AKnight, AKnave)`
- No person is both: `Not(And(AKnight, AKnave))`
- If A is a Knight, their statement is true: `Implication(AKnight, statement)`
- If A is a Knave, their statement is false: `Implication(AKnave, Not(statement))`

## License

This project is open source and available for educational purposes.

## Author

Created as part of a logic and AI course project.

