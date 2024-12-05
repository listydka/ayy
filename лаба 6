import time
import itertools as it
import copy as c

def generate_algorithmic(matrix, n):
    """Алгоритмическая генерация вариантов."""
    results = []
    matrix_copy = c.deepcopy(matrix)
    minus = n - 1
    for flag in range(n):
        for i in range(n):
            if i != flag:
                save = matrix_copy[i][i]
                matrix_copy[i][i] = matrix_copy[i][minus]
                matrix_copy[i][minus] = save
            minus -= 1
        results.append(c.deepcopy(matrix_copy))
        matrix_copy = c.deepcopy(matrix)
        minus = n - 1
    return results

def generate_itertools(matrix, n):
    """Генерация вариантов с помощью itertools."""
    main_diagonal = [matrix[i][i] for i in range(n)]
    secondary_diagonal = [matrix[i][n - i - 1] for i in range(n)]
    permutations = list(it.permutations(range(n), 2))
    results = []

    for flag in range(n):
        for perm in permutations:
            matrix_copy = c.deepcopy(matrix)
            for i in range(n):
                if i != flag:
                    matrix_copy[i][i] = main_diagonal[perm[0]]
                    matrix_copy[i][n - i - 1] = secondary_diagonal[perm[1]]
            results.append(matrix_copy)
    return results

def apply_constraints(matrix, n, threshold):
    """Применение ограничения и целевой функции."""
    results = []
    optimal_matrix = None
    optimal_sum = float('inf')

    for mat in matrix:
        main_diagonal_sum = sum(mat[i][i] for i in range(n))
        if main_diagonal_sum < threshold and main_diagonal_sum < optimal_sum:
            optimal_matrix = mat
            optimal_sum = main_diagonal_sum
        if main_diagonal_sum < threshold:
            results.append(mat)

    return results, optimal_matrix, optimal_sum

def print_matrix(matrix):
    """Печать матрицы в удобном виде."""
    return '\n'.join('\t'.join(map(str, row)) for row in matrix)

def main():
    n = int(input("Введите размер квадратной матрицы (n): "))
    matrix = [[(j + 1) * (i + 1) for j in range(n)] for i in range(n)]
    print("Исходная матрица:")
    print(print_matrix(matrix))

    # 1 часть: генерация вариантов двумя способами
    print("\n--- Генерация алгоритмическим способом ---")
    start_time = time.time()
    algo_results = generate_algorithmic(matrix, n)
    algo_time = time.time() - start_time
    print(f"Сгенерировано {len(algo_results)} вариантов за {algo_time:.5f} секунд.")

    print("\n--- Генерация с помощью itertools ---")
    start_time = time.time()
    itertools_results = generate_itertools(matrix, n)
    itertools_time = time.time() - start_time
    print(f"Сгенерировано {len(itertools_results)} вариантов за {itertools_time:.5f} секунд.")

    # 2 часть: усложнение с ограничением и целевой функцией
    print("\n--- Усложнение программы ---")
    threshold = n * n  # Ограничение: сумма главной диагонали меньше n^2
    filtered_results, optimal_matrix, optimal_sum = apply_constraints(itertools_results, n, threshold)
    print(f"Сгенерировано {len(filtered_results)} вариантов, удовлетворяющих ограничению.")
    print(f"Оптимальная матрица с минимальной суммой диагонали ({optimal_sum}):")
    print(print_matrix(optimal_matrix))

if __name__ == "__main__":
    main()
