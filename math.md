
# Mathematics Notes

## 1. Arithmetic & Algebra

### Numbers
- Natural: N = {1,2,3,...}
- Integers: Z = {...,-2,-1,0,1,2,...}
- Rational: Q = p/q
- Real: R, Complex: C

### Powers & Logarithms
- a^m * a^n = a^(m+n)
- (a^m)^n = a^(mn)
- log_a(xy) = log_a(x) + log_a(y)
- log_a(x^r) = r * log_a(x)

### Series
- Sum of n: S = n(n+1)/2
- Sum of squares: S = n(n+1)(2n+1)/6
- Sum of cubes: S = [n(n+1)/2]^2
- Geometric: a(1-r^n)/(1-r)

### Polynomials & Complex Numbers
- (a+b)^2 = a^2+2ab+b^2
- a^2-b^2 = (a-b)(a+b)
- i^2 = -1, z = a+bi
- |z| = sqrt(a^2+b^2)

---

## 2. Geometry & Trigonometry

### Distance
- d = sqrt((x2-x1)^2+(y2-y1)^2)

### Area
- Triangle: (1/2)bh
- Circle: πr^2

### Trig Identities
- sin^2θ+cos^2θ = 1
- sin(α±β) = sinαcosβ ± cosαsinβ
- cos(α±β) = cosαcosβ ∓ sinαsinβ

---

## 3. Linear Algebra

### Vectors
- Dot: a·b = Σ a_i b_i
- Cross (3D): a×b = |i  j  k; a1 a2 a3; b1 b2 b3|
- Norm: ||a|| = sqrt(a·a)

### Matrices
- Transpose: A^T
- Inverse: A^-1 such that AA^-1 = I
- Determinant (2x2): ad-bc
- Multiplication: (AB)_ij = Σ A_ik B_kj

### Decompositions
- LU, QR, SVD

---

## 4. Calculus & Optimization

### Limits
- lim x->a f(x)

### Derivatives
- d/dx x^n = n x^(n-1)
- Chain rule: (f(g(x)))' = f'(g(x))g'(x)

### Integrals
- ∫ x^n dx = x^(n+1)/(n+1)
- Definite: ∫_a^b f(x) dx

### Multivariable
- Gradient: ∇f = (∂f/∂x1, ..., ∂f/∂xn)
- Hessian: matrix of 2nd derivatives

### Optimization
- Convex sets/functions
- Gradient descent: θ := θ - η∇f(θ)

---

## 5. Probability & Statistics

### Probability
- P(A∪B) = P(A)+P(B)-P(A∩B)
- Bayes: P(A|B)=P(B|A)P(A)/P(B)

### Random Variables
- E[X] = Σ xP(x)
- Var(X) = E[X^2]-E[X]^2

### Distributions
- Bernoulli(p), Binomial(n,p)
- Normal(μ,σ^2): pdf = (1/(σ√2π))e^(-(x-μ)^2/(2σ^2))

### Information Theory
- Entropy: H(X) = -Σ p(x) log p(x)
- KL Divergence: D_KL(P||Q) = Σ P(x) log(P(x)/Q(x))

---

## 6. Discrete Math & DSA

### Combinatorics
- Permutations: P(n,k)=n!/(n-k)!
- Combinations: C(n,k)=n!/(k!(n-k)!)

### Graph Theory
- Graph G(V,E), Degree, Paths, Cycles
- Adjacency Matrix, BFS, DFS

### Number Theory
- GCD via Euclid
- Modular Arithmetic: (a+b) mod m, (ab) mod m

---

## 7. Advanced Topics

### Linear Transformations & Tensors
- Tensor: multilinear map
- Rank, Trace of matrix

### Manifolds (Basics)
- Locally Euclidean spaces

### Optimization in ML
- Lagrange Multipliers: L(x,λ) = f(x)+λg(x)
- Convex optimization properties
