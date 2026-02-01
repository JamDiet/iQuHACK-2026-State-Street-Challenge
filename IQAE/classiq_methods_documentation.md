# Classiq SDK Methods and Import Guide

This document provides a comprehensive overview of the methods and classes you can import and use from the Classiq Python SDK.

## Core Workflow Functions

### Modeling
```python
from classiq import create_model, write_qmod, qasm_to_qmod, QmodFormat
```

- **`create_model(main_func)`** - Create a quantum model from a decorated function
- **`write_qmod(model, file_path)`** - Write a quantum model to a file
- **`qasm_to_qmod(qasm_str)`** - Convert QASM to Qmod format
- **`QmodFormat`** - Enum for Qmod format types

### Synthesis
```python
from classiq import (
    synthesize,
    synthesize_async,
    show,
    QuantumProgram,
    Preferences,
    Constraints,
    set_preferences,
    set_constraints,
    set_execution_preferences,
    update_preferences,
    update_constraints,
    update_execution_preferences
)
```

- **`synthesize(model)`** - Synthesize a quantum model into a quantum program
- **`synthesize_async(model)`** - Async version of synthesize
- **`show(qprog)`** - Visualize the quantum program in the IDE
- **`QuantumProgram`** - Class representing a synthesized quantum program
- **`Preferences`** - Class for synthesis preferences (optimization level, etc.)
- **`Constraints`** - Class for circuit constraints (max width, max depth, etc.)
- **`set_preferences(model, preferences)`** - Set synthesis preferences
- **`set_constraints(model, constraints)`** - Set circuit constraints
- **`set_execution_preferences(model, prefs)`** - Set execution preferences

### Execution
```python
from classiq import (
    execute,
    execute_async,
    ExecutionPreferences,
    BackendPreferences,
    ExecutionSession,
    assign_parameters,
    transpile,
    set_quantum_program_execution_preferences
)
```

- **`execute(qprog)`** - Execute a quantum program
- **`execute_async(qprog)`** - Async version of execute
- **`ExecutionPreferences`** - Class for execution settings (num_shots, etc.)
- **`BackendPreferences`** - Backend selection and configuration
- **`ExecutionSession`** - Session management for multiple executions
- **`assign_parameters(qprog, params)`** - Assign parameter values to a quantum program
- **`transpile(qprog, backend)`** - Transpile to specific backend
- **`set_quantum_program_execution_preferences(qprog, prefs)`** - Set execution preferences on program

## Qmod Language Constructs

### Decorators
```python
from classiq import qfunc, qperm, cfunc
```

- **`@qfunc`** - Decorator for quantum functions
  - `@qfunc(synthesize_separately=True)` - Synthesize function separately
- **`@qperm`** - Decorator for quantum permutations (uncompute automatically)
- **`@cfunc`** - Decorator for classical functions

### Quantum Types
```python
from classiq import QBit, QNum, QArray, QStruct, Const, Input, Output
```

- **`QBit`** - Single quantum bit type
- **`QNum`** - Quantum number register type
- **`QArray`** - Array of quantum bits
- **`QStruct`** - Structured quantum data type
- **`Const`** - Mark parameter as constant (won't be modified)
- **`Input`** - Mark parameter as input
- **`Output`** - Mark parameter as output

### Classical Types
```python
from classiq import CInt, CReal, CBool, CArray
```

- **`CInt`** - Classical integer parameter
- **`CReal`** - Classical real number parameter
- **`CBool`** - Classical boolean parameter
- **`CArray`** - Classical array parameter

### Quantum Callables
```python
from classiq import QCallable, QCallableList, QPerm, QPermList
```

- **`QCallable`** - Type for quantum function references
- **`QCallableList`** - List of quantum callables
- **`QPerm`** - Type for quantum permutation references
- **`QPermList`** - List of quantum permutations

## Basic Quantum Operations

### Single-Qubit Gates
```python
from classiq import H, X, Y, Z, S, T, RX, RY, RZ, U
```

- **`H(target)`** - Hadamard gate
- **`X(target)`** - Pauli-X (NOT) gate
- **`Y(target)`** - Pauli-Y gate
- **`Z(target)`** - Pauli-Z gate
- **`S(target)`** - S gate (phase gate)
- **`T(target)`** - T gate (π/8 gate)
- **`RX(theta, target)`** - Rotation around X axis
- **`RY(theta, target)`** - Rotation around Y axis
- **`RZ(theta, target)`** - Rotation around Z axis
- **`U(theta, phi, lam, target)`** - Universal single-qubit gate

### Multi-Qubit Gates
```python
from classiq import CX, CZ, SWAP, CRX, CRY, CRZ
```

- **`CX(control, target)`** - CNOT gate
- **`CZ(control, target)`** - Controlled-Z gate
- **`SWAP(target1, target2)`** - SWAP gate
- **`CRX(theta, control, target)`** - Controlled RX
- **`CRY(theta, control, target)`** - Controlled RY
- **`CRZ(theta, control, target)`** - Controlled RZ

### Control Operations
```python
from classiq import control, power, invert, within_apply
```

- **`control(ctrl_qubits, operation)`** - Apply controlled operation
- **`power(n, operation)`** - Apply operation n times
- **`invert(operation)`** - Invert/uncompute operation
- **`within_apply(within_func, apply_func)`** - Within-apply pattern

## High-Level Quantum Functions

### State Preparation
```python
from classiq import (
    prepare_state,
    prepare_amplitudes,
    inplace_prepare_state,
    prepare_uniform_superposition
)
```

- **`prepare_state(probabilities, target)`** - Prepare arbitrary state
- **`prepare_amplitudes(amplitudes, bound, target)`** - Prepare state from amplitudes
- **`inplace_prepare_state(probabilities, bound, target)`** - In-place state preparation
- **`prepare_uniform_superposition(target)`** - Prepare uniform superposition

### Arithmetic Operations
```python
from classiq import (
    add,
    subtract,
    multiply,
    divide,
    inplace_add,
    inplace_subtract
)
```

- **`add(a, b, result)`** - Quantum addition
- **`subtract(a, b, result)`** - Quantum subtraction
- **`multiply(a, b, result)`** - Quantum multiplication
- **`divide(a, b, result)`** - Quantum division
- **`inplace_add(a, b)`** - In-place addition
- **`inplace_subtract(a, b)`** - In-place subtraction

### Comparison Operations
```python
from classiq import compare, is_equal, is_greater, is_less
```

- **`compare(a, b, operator, result)`** - Compare quantum numbers
  - Operators: `"EQ"`, `"NE"`, `"GT"`, `"GE"`, `"LT"`, `"LE"`
- **`is_equal(a, b, result)`** - Check equality
- **`is_greater(a, b, result)`** - Check if greater
- **`is_less(a, b, result)`** - Check if less

### Quantum Register Allocation
```python
from classiq import allocate, allocate_num, drop
```

- **`allocate(size, target)`** - Allocate quantum register
- **`allocate_num(size, is_signed, fraction_digits, target)`** - Allocate quantum number
- **`drop(target)`** - Drop/free quantum register

### Oracle and Phase Operations
```python
from classiq import apply_to_all, flip_msb, phase_oracle
```

- **`apply_to_all(gate, target)`** - Apply gate to all qubits
- **`flip_msb(target)`** - Flip most significant bit
- **`phase_oracle(oracle_func, target)`** - Create phase oracle

## Advanced Quantum Functions

### Quantum Fourier Transform
```python
from classiq import qft, iqft
```

- **`qft(target)`** - Quantum Fourier Transform
- **`iqft(target)`** - Inverse QFT

### Amplitude Estimation
```python
from classiq import grover_operator, grover_diffusion_operator
```

- **`grover_operator(oracle, target)`** - Grover operator
- **`grover_diffusion_operator(target)`** - Diffusion operator

### Quantum Search
```python
from classiq import swap_test
```

- **`swap_test(state1, state2, test)`** - Swap test for state overlap

## Applications

### Combinatorial Optimization
```python
from classiq.applications.combinatorial_optimization import (
    CombinatorialProblem,
    construct_combinatorial_optimization_model,
    execute_qaoa,
    compute_qaoa_initial_point,
    pyo_model_to_hamiltonian
)
```

### Amplitude Estimation (IQAE)
```python
from classiq.applications.iqae.iqae import IQAE
```

- **`IQAE`** - Iterative Quantum Amplitude Estimation class

### Hamiltonian Tools
```python
from classiq.applications.hamiltonian.pauli_decomposition import (
    hamiltonian_to_matrix,
    matrix_to_hamiltonian,
    matrix_to_pauli_operator,
    pauli_operator_to_matrix
)
```

## Utility Functions

### Authentication and Configuration
```python
from classiq import authenticate, configure
```

- **`authenticate()`** - Authenticate with Classiq platform
- **`configure()`** - Configure SDK settings

### Help and Documentation
```python
from classiq import open_help
```

- **`open_help()`** - Open Classiq documentation

### Analyzer
```python
from classiq import Analyzer
```

- **`Analyzer`** - Circuit analysis tools

## Constants and Enums

```python
from classiq import SIGNED, UNSIGNED, ControlState, RegisterUserInput
```

- **`SIGNED`** - Constant for signed quantum numbers
- **`UNSIGNED`** - Constant for unsigned quantum numbers
- **`ControlState`** - Enum for control state configuration
- **`RegisterUserInput`** - Register configuration class

## Common Import Pattern

For most Classiq projects, you'll typically use:

```python
from classiq import *
```

This imports all commonly used functions and classes. However, for specific applications, you might want selective imports:

```python
# Core workflow
from classiq import (
    qfunc,
    QBit,
    QNum,
    QArray,
    create_model,
    synthesize,
    execute,
    show
)

# Quantum operations
from classiq import H, X, CX, control, power

# State preparation
from classiq import prepare_state, prepare_amplitudes

# Arithmetic
from classiq import inplace_add, compare

# Applications
from classiq.applications.iqae.iqae import IQAE
```

## Example Usage

### Basic Circuit
```python
from classiq import *

@qfunc
def main(x: Output[QBit]):
    allocate(1, x)
    H(x)

model = create_model(main)
qprog = synthesize(model)
show(qprog)
result = execute(qprog).result()
```

### With Quantum Numbers
```python
from classiq import *

@qfunc
def main(a: Output[QNum], b: Output[QNum], res: Output[QBit]):
    prepare_int(5, a)
    prepare_int(3, b)
    compare(a, b, "GT", res)

model = create_model(main)
qprog = synthesize(model)
result = execute(qprog).result()
```

## Documentation Resources

- **Online Docs**: https://docs.classiq.io
- **Agent-Friendly Docs**: https://docs.classiq.io/latest/llms.txt
- **Local Library**: `/home/workspace/Documents/classiq-library`
- **SDK Location**: `/home/openvscode-server/classiq-venv/lib/python3.12/site-packages/classiq`

## Best Practices

1. **Use high-level functions** - Prefer Classiq's built-in functions over manual gate-level programming
2. **Leverage synthesis** - Let Classiq optimize your circuits automatically
3. **Set constraints** - Use `Constraints` to control circuit properties (width, depth)
4. **Explore examples** - Check `classiq-library` for patterns and templates
5. **Use decorators** - `@qfunc` for quantum functions, `@qperm` for uncomputable operations
6. **Type your parameters** - Use `QBit`, `QNum`, `QArray` for clarity and type safety
