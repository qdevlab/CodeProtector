# CodeProtector

LLVM-обфускатор для защиты кода и данных от реверс-инжиниринга.

LLVM obfuscator for protecting code and data against reverse engineering.

---

CodeProtector — многоуровневый обфускатор на базе LLVM (версии 18–20). Усложняет статический и динамический анализ, а также модификацию собранного программного обеспечения. Обфускация выполняется автоматически на этапе компиляции на уровне LLVM IR, без изменения исходного кода. Поддерживаются Windows (MSVC + clang-cl) и Linux (Clang + lld), архитектуры x86 и x86_64.

### Функционал

Обфускация данных: шифрование строковых литералов с расшифровкой в runtime на стеке, замена числовых констант на вычисляемые выражения, шифрование глобальных переменных с ленивой расшифровкой при первом доступе.

Обфускация кода: уплощение потока управления (control flow flattening), вставка ложных ветвлений с непрозрачными предикатами, подстановка эквивалентных инструкций, вставка мёртвого кода, разбиение и слияние функций. На уровне бэкенда — полиморфная замена машинных инструкций и обфускация прологов/эпилогов.

Обфускация настраивается глобально через флаги компилятора и точечно через директивы в коде. Позволяет выбрать конкретные техники для отдельной функции. Модули и функции можно полностью исключить из обфускации. Фиксированное начальное значение (seed) обеспечивает воспроизводимость сборок для отладки.

### Результаты

Реализован набор LLVM-пассов, покрывающий обфускацию данных, потока управления и машинного кода. Обфускатор прошёл апробацию на коммерческом продукте компании.

### Роль

Архитектура обфускатора, проектирование механизмов защиты

Проект закрытый, коммерческий.

### Ограничения

Обфускация применяется только к проектам, успешно компилируемым Clang.
Замедляет работу защищённого ПО, требует профилирования для исключения горячих функций.
Требует тестирования базового функционала после обфускации.

***

### Overview

CodeProtector is a multi-layered obfuscator built on LLVM (ver. 18–20). It impedes static and dynamic analysis as well as modification of compiled software. Obfuscation is applied automatically at compile time at the LLVM IR level, with no changes to the source code. Supported environments: Windows (MSVC + clang-cl) and Linux (Clang + lld), x86 and x86_64 architectures.

### Features

Data obfuscation: encryption of string literals with runtime decryption on the stack, replacement of numeric constants with computed expressions, encryption of global variables with lazy decryption on first access.

Code obfuscation: control flow flattening, insertion of bogus branches with opaque predicates, equivalent instruction substitution, dead code insertion, function splitting and merging. At the backend level — polymorphic machine instruction substitution and prologue/epilogue obfuscation.

Obfuscation is configured globally via compiler flags and per-function via source code directives. Specific techniques can be selected for individual functions. Modules and functions can be fully excluded from obfuscation. A fixed seed value ensures reproducible builds for debugging.

### Results

A set of LLVM passes was implemented covering data obfuscation, control flow obfuscation, and machine code obfuscation. The obfuscator was validated on a commercial product of the company.

### Role

Obfuscator architecture, design of protection mechanisms.

A closed, commercial project.

### Limitations

Obfuscation is only applicable to projects that compile successfully with Clang. It introduces runtime performance overhead, requiring profiling to identify and exclude hot functions. 
Core functionality must be retested after obfuscation.

***

