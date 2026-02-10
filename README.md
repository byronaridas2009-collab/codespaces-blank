# =========================================
# CORRECTED SELF-LEARNING MATH AI
# Python 3.13
# =========================================

import random
from sympy import symbols, solve, sympify, Eq

x = symbols('x')

# ---------------------------------
# PART 1: SYMBOLIC MATH SOLVER
# ---------------------------------

def solve_math(problem: str):
    """
    Solves algebraic equations.
    Accepts:
      x**2 - 4
      x**2 - 4 = 0
    """
    try:
        if "=" in problem:
            left, right = problem.split("=")
            expr = Eq(sympify(left), sympify(right))
        else:
            expr = sympify(problem)

        return solve(expr, x)

    except Exception as e:
        return f"Invalid math input: {e}"

# ---------------------------------
# PART 2: SIMPLE LEARNING AI
# (Learns average correction)
# ---------------------------------

class LearningAI:
    def __init__(self):
        self.bias = 0.0
        self.learning_rate = 0.01

    def predict(self, a, b):
        return a + b + self.bias

    def train(self, rounds=500):
        for _ in range(rounds):
            a = random.randint(1, 20)
            b = random.randint(1, 20)

            prediction = self.predict(a, b)
            target = a + b

            error = target - prediction
            self.bias += self.learning_rate * error

    def stats(self):
        return f"Current bias: {self.bias:.4f}"

# ---------------------------------
# PART 3: CLI INTERFACE
# ---------------------------------

def main():
    learner = LearningAI()

    print("🧠 Math AI (Python 3.13)")
    print("Solve equations like:")
    print("  x**2 - 4")
    print("  x**2 - 5*x + 6 = 0")
    print("Commands: train | stats | exit")
    print("-" * 40)

    while True:
        user_input = input(">>> ").strip()

        if user_input == "exit":
            print("Goodbye 👋")
            break

        elif user_input == "train":
            learner.train()
            print("AI trained.")

        elif user_input == "stats":
            print(learner.stats())

        else:
            result = solve_math(user_input)
            print("Solution:", result)

# ---------------------------------
# RUN
# ---------------------------------

if __name__ == "__main__":
    main()
