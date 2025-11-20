# ================================
# Project: EdgeLab
# Description:
# Where cuttedge concepts meet clean implementation.
# This repository explores modern patterns, performance, and scalability.
# ================================

# ---------- main.py ----------
"""
Main entry point for EdgeLab.
"""

from core import performance, patterns


def run():
    print("⚙️  Welcome to EdgeLab")
    print("🧠 Exploring Modern Patterns | 🚀 Performance | ♾️ Scalability\n")

    # Demo functionality
    data = [10, 20, 30, 40, 50]
    print("🔁 Functional Map Demo:", patterns.apply_pattern(lambda x: x * 2, data))
    print("⚡ Performance Metric:", performance.benchmark(lambda: sum(range(1_000_000))))
    print("🏗️ Scalable Aggregation:", performance.chunk_sum(data, chunk_size=2))


if __name__ == "__main__":
    run()


# ---------- core/patterns.py ----------
"""
Module demonstrating clean and modern coding patterns.
Includes functional, modular, and object-oriented examples.
"""

from typing import Callable, List, Any

def apply_pattern(func: Callable[[Any], Any], items: List[Any]) -> List[Any]:
    """Apply a function to each item in a list (functional pattern)."""
    return [func(i) for i in items]

class SingletonMeta(type):
    """Metaclass implementing the Singleton design pattern."""
    _instances = {}
    def __call__(cls, *args, **kwargs):
        if cls not in cls._instances:
            cls._instances[cls] = super().__call__(*args, **kwargs)
        return cls._instances[cls]

class Config(metaclass=SingletonMeta):
    """Global configuration (Singleton)."""
    def __init__(self, name="EdgeLab", version="1.0"):
        self.name = name
        self.version = version


# ---------- core/performance.py ----------
"""
Performance and scalability utilities.
Includes benchmarking and efficient data processing tools.
"""

import time
from typing import Callable, List

def benchmark(func: Callable, *args, **kwargs) -> str:
    """Measure execution time for a given function."""
    start = time.perf_counter()
    func(*args, **kwargs)
    end = time.perf_counter()
    duration = round((end - start) * 1000, 3)
    return f"{duration} ms"

def chunk_sum(data: List[int], chunk_size: int = 3) -> List[int]:
    """Efficiently sum data in chunks (scalable pattern)."""
    return [sum(data[i:i + chunk_size]) for i in range(0, len(data), chunk_size)]


# ---------- tests/test_patterns.py ----------
"""
Tests for patterns.py module.
Run with: pytest
"""

from core import patterns

def test_apply_pattern():
    result = patterns.apply_pattern(lambda x: x + 1, [1, 2, 3])
    assert result == [2, 3, 4]

def test_singleton():
    c1 = patterns.Config()
    c2 = patterns.Config()
    assert c1 is c2
    assert c1.name == "EdgeLab"

