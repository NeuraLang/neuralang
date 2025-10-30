# Contributing to Neura

Thank you for your interest in contributing to Neura! We're building a cutting-edge programming language for AI and machine learning, and we welcome contributions from developers, researchers, and ML practitioners.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Setup](#development-setup)
- [How to Contribute](#how-to-contribute)
- [Coding Standards](#coding-standards)
- [Testing Guidelines](#testing-guidelines)
- [Commit Message Conventions](#commit-message-conventions)
- [Pull Request Process](#pull-request-process)
- [Project Structure](#project-structure)
- [License](#license)

## Code of Conduct

By participating in this project, you agree to maintain a respectful and inclusive environment for all contributors. We are committed to providing a welcoming experience for everyone, regardless of background or level of experience.

### Our Standards

- **Be respectful**: Treat all contributors with respect and consideration
- **Be collaborative**: Work together to build the best solution
- **Be constructive**: Provide helpful feedback and accept constructive criticism
- **Be patient**: Remember that everyone has different experience levels
- **Be inclusive**: Welcome newcomers and help them get started

## Getting Started

### Prerequisites

- **Rust 1.70+**: Install from [rustup.rs](https://rustup.rs/)
- **LLVM**: Required for compiler backend
- **CUDA Toolkit** (optional): For GPU support development
- **Git**: For version control

### Development Setup

1. **Fork and clone the repository**:
   ```bash
   git clone https://github.com/YOUR_USERNAME/neura.git
   cd neura
   ```

2. **Add upstream remote**:
   ```bash
   git remote add upstream https://github.com/andreimotin/neura.git
   ```

3. **Install dependencies**:
   ```bash
   cargo build
   ```

4. **Run tests to verify setup**:
   ```bash
   cargo test
   ```

5. **Run the REPL** (once implemented):
   ```bash
   cargo run --bin neura repl
   ```

## How to Contribute

### Types of Contributions

We welcome many types of contributions:

- **Bug fixes**: Help us identify and fix issues
- **Feature implementation**: Work on planned features from our roadmap
- **Documentation**: Improve docs, add examples, write tutorials
- **Testing**: Add test cases, improve test coverage
- **Performance improvements**: Optimize existing code
- **Code reviews**: Review pull requests from other contributors

### Finding Work

1. Check our [task-list.md](task-list.md) for planned features
2. Look for issues labeled `good first issue` or `help wanted`
3. Review our [roadmap](README.md#-roadmap) for upcoming features
4. Propose new features by opening an issue first

### Before You Start

- **Check existing issues**: Make sure someone isn't already working on it
- **Open an issue**: For significant changes, discuss your approach first
- **Keep it focused**: One feature or fix per pull request
- **Follow conventions**: Use our coding standards and commit format

## Coding Standards

### Rust Style Guidelines

Follow the official [Rust Style Guide](https://doc.rust-lang.org/style-guide/):

- Use `rustfmt` for automatic formatting: `cargo fmt`
- Use `clippy` for linting: `cargo clippy`
- Write idiomatic Rust code
- Prefer explicit types for public APIs
- Document all public functions, types, and modules

### Code Organization

- **Keep files under 200-300 lines**: Refactor when files grow too large
- **Avoid duplication**: Check for similar functionality before implementing
- **Simple solutions**: Prefer simple, maintainable code over clever solutions
- **No dead code**: Remove unused imports, functions, and comments
- **Environment awareness**: Code should work across dev, test, and prod

### Documentation

- **Public APIs**: Document all public functions, structs, enums, and traits
- **Examples**: Include usage examples in doc comments
- **Complex logic**: Add inline comments explaining non-obvious code
- **Module-level docs**: Every module should have a module-level doc comment

Example:
```rust
/// Performs shape inference for tensor operations.
///
/// # Arguments
///
/// * `left_shape` - Shape of the left operand
/// * `right_shape` - Shape of the right operand
/// * `operation` - The tensor operation being performed
///
/// # Returns
///
/// The inferred output shape or a type error
///
/// # Examples
///
/// ```
/// let shape = infer_shape(&[64, 784], &[784, 10], TensorOp::MatMul)?;
/// assert_eq!(shape, vec![64, 10]);
/// ```
pub fn infer_shape(
    left_shape: &[usize],
    right_shape: &[usize],
    operation: TensorOp,
) -> Result<Vec<usize>, TypeError> {
    // Implementation
}
```

### Error Handling

- Use `Result<T, E>` for fallible operations
- Define clear, descriptive error types
- Provide helpful error messages for ML-specific errors
- Include source location information in parser/compiler errors

## Testing Guidelines

### Test Requirements

All contributions must include appropriate tests:

- **Unit tests**: Test individual functions and components
- **Integration tests**: Test feature workflows end-to-end
- **Parser tests**: Test syntax parsing with various examples
- **Type system tests**: Test type checking and shape inference
- **Tensor operation tests**: Verify correctness of ML operations

### Test Organization

- **Unit tests**: Place alongside the code in the same file (using `#[cfg(test)]`)
- **Integration tests**: Place in the `tests/` directory
- **Example tests**: Ensure example `.neura` files are valid

### Running Tests

```bash
# Run all tests
cargo test

# Run specific test
cargo test test_name

# Run tests with output
cargo test -- --nocapture

# Run tests for a specific module
cargo test module_name

# Run benchmarks
cargo bench
```

### Writing Good Tests

```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_tensor_matmul_shape_inference() {
        let left = TensorType::new(vec![64, 784], DataType::Float32);
        let right = TensorType::new(vec![784, 10], DataType::Float32);
        
        let result = infer_matmul_shape(&left, &right).unwrap();
        
        assert_eq!(result.shape, vec![64, 10]);
        assert_eq!(result.dtype, DataType::Float32);
    }

    #[test]
    fn test_invalid_matmul_shape() {
        let left = TensorType::new(vec![64, 784], DataType::Float32);
        let right = TensorType::new(vec![100, 10], DataType::Float32);
        
        let result = infer_matmul_shape(&left, &right);
        
        assert!(result.is_err());
    }
}
```

## Commit Message Conventions

We follow [Conventional Commits](https://www.conventionalcommits.org/) format:

### Format

```
<type>: <subject>

<body>

<footer>
```

### Types

- `feat`: New feature implementation
- `fix`: Bug fix
- `refactor`: Code refactoring without behavior change
- `docs`: Documentation updates
- `test`: Adding or updating tests
- `perf`: Performance improvements
- `chore`: Maintenance tasks (dependencies, configs)
- `style`: Code formatting changes

### Examples

```bash
# Simple commit
git commit -m "feat: implement basic tensor addition operation"

# Detailed commit with body
git commit -m "feat: add shape inference for tensor operations" \
           -m "- Implements compile-time shape checking" \
           -m "- Adds support for broadcasting rules" \
           -m "- Includes comprehensive test suite" \
           -m "Related to task 2.4 in task-list.md"
```

### Guidelines

- Use present tense: "add feature" not "added feature"
- Keep subject line under 72 characters
- Start with lowercase (except for proper nouns)
- No period at the end of the subject line
- Separate subject from body with blank line
- Use body to explain what and why, not how
- Reference issues and task numbers when applicable

## Pull Request Process

### Before Submitting

1. **Update your branch**:
   ```bash
   git fetch upstream
   git rebase upstream/main
   ```

2. **Ensure all tests pass**:
   ```bash
   cargo test
   cargo clippy
   cargo fmt -- --check
   ```

3. **Update documentation**: Update relevant docs and examples

4. **Clean up commits**: Squash or organize commits logically

### PR Guidelines

1. **Create from a feature branch**: Never from `main`
2. **Use a descriptive title**: Follow commit message conventions
3. **Fill out the PR template**: Explain what, why, and how
4. **Link related issues**: Use "Fixes #123" or "Relates to #456"
5. **Keep PRs focused**: One feature or fix per PR
6. **Request reviews**: Tag relevant maintainers

### PR Template

```markdown
## Description
Brief description of changes

## Motivation
Why is this change needed?

## Changes
- List of key changes
- Another change
- One more change

## Testing
- [ ] Unit tests added/updated
- [ ] Integration tests pass
- [ ] Manual testing performed

## Checklist
- [ ] Code follows project style guidelines
- [ ] Documentation updated
- [ ] Tests pass locally
- [ ] Commit messages follow conventions
- [ ] No breaking changes (or documented if necessary)

## Related Issues
Fixes #123
Relates to task X.Y in task-list.md
```

### Review Process

- All PRs require at least one approval from a maintainer
- Address review feedback promptly
- Be open to suggestions and discussions
- Once approved, a maintainer will merge your PR

## Project Structure

```
neura/
├── src/
│   ├── main.rs                    # Entry point
│   ├── parser/                    # Parser implementation
│   │   ├── mod.rs
│   │   └── grammar.pest           # PEG grammar
│   ├── ast/                       # Abstract Syntax Tree
│   ├── compiler/                  # Compiler infrastructure
│   ├── codegen/                   # Code generation
│   │   └── cuda.rs               # CUDA codegen
│   ├── typesystem/                # Type system
│   │   └── tensor.rs             # Tensor types
│   ├── runtime/                   # Runtime components
│   │   ├── tensor.rs             # Tensor operations
│   │   ├── autodiff.rs           # Auto differentiation
│   │   └── cuda_bindings.rs      # CUDA FFI
│   ├── repl/                      # REPL environment
│   ├── interop/                   # Interoperability
│   │   └── python.rs             # Python bindings
│   └── ml/                        # ML primitives
│       ├── primitives.rs         # Layers, activations
│       └── data_pipeline.rs      # Data processing
├── tests/                         # Integration tests
├── examples/                      # Example .neura programs
├── docs/                          # Documentation
├── Cargo.toml                     # Dependencies
└── README.md                      # Project overview
```

## License

By contributing to Neura, you agree that your contributions will be licensed under the [Apache License 2.0](LICENSE).

### Apache 2.0 Summary

- **Permissions**: Commercial use, modification, distribution, patent use, private use
- **Conditions**: License and copyright notice, state changes
- **Limitations**: Liability, warranty, trademark use

### Contributor License Agreement

By submitting a pull request, you represent that:

1. You have the right to submit the contribution
2. Your contribution is your original creation
3. You grant the project a perpetual, worldwide, non-exclusive license to use your contribution
4. Your contribution is licensed under Apache 2.0

## Questions?

- **Open an issue**: For bugs, feature requests, or questions
- **Check documentation**: Review [README.md](README.md) and [neura-spec.md](neura-spec.md)
- **Ask for help**: Don't hesitate to ask questions in your PR or issue

---

**Thank you for contributing to Neura! Together we're building the future of ML programming.** 🚀


