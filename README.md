# Отчёт по ЛР №1 – Boost
## Шаг 1. Скачивание Boost
Файл: step1_wget.txt

Команда:
```sh
cd ~
wget -O boost_1_69_0.tar.gz https://archives.boost.io/release/1.69.0/source/boost_1_69_0.tar.gz | tee step1_wget.txt
```



## Шаг 2. Распаковка архива

Файл: step2_ls_dir.txt

Команда:
```sh
tar -xzf boost_1_69_0.tar.gz 2>&1 | tee step2_ls_dir.txt
ls -ld ~/boost_1_69_0 | tee -a step2_ls_dir.txt
```



## Шаг 3. Количество файлов без вложенных директорий

Файл: step3_count_no_recursive.txt

Команда:
```sh
find ~/boost_1_69_0 -maxdepth 1 -type f | tee step3_files_no_recursive.txt | wc -l | tee step3_count_no_recursive.txt
```
## Шаг 4. Количество файлов со всеми вложенными директориями

Файл: step4_count_all.txt

Команда:
```sh
find ~/boost_1_69_0 -type f | tee step4_files_all.txt | wc -l | tee step4_count_all.txt
```

## Шаг 5. Подсчёт .hpp, .cpp и остальных файлов

Файл: step5_hpp.txt, step5_cpp.txt, step5_other_count.txt

Команды:
```sh
find ~/boost_1_69_0 -type f -name "*.hpp" | tee step5_hpp.txt | wc -l
find ~/boost_1_69_0 -type f -name "*.cpp" | tee step5_cpp.txt | wc -l
TOTAL=$(find ~/boost_1_69_0 -type f | wc -l)
HPP=$(find ~/boost_1_69_0 -type f -name "*.hpp" | wc -l)
CPP=$(find ~/boost_1_69_0 -type f -name "*.cpp" | wc -l)
echo $((TOTAL - HPP - CPP)) | tee step5_other_count.txt
```

## Шаг 6. Полный путь до any.hpp

Файл: step6_any.txt

Команда:
```sh
find ~/boost_1_69_0 -name "any.hpp" | tee step6_any.txt
```

## Шаг 7. Файлы, где встречается boost::asio

Файл: step7_asio.txt

Команда:
```sh
grep -Rsl "boost::asio" ~/boost_1_69_0 | tee step7_asio.txt
```


## Шаг 8. Компиляция Boost

Файл: step8_bootstrap.txt, step8_build.txt

Команды:
```sh
cd ~/boost_1_69_0
./bootstrap.sh | tee step8_bootstrap.txt
./b2 | tee step8_build.txt
```



## Шаг 9. Перенос статических библиотек

Файл: step9_copy_libs.txt, step9_count_libs.txt

Команды:

```sh
mkdir -p ~/boost-libs
find ~/boost_1_69_0 -name "*.a" -type f -exec cp -t ~/boost-libs {} + 2>&1 | tee step9_copy_libs.txt
ls -1 ~/boost-libs | wc -l | tee step9_count_libs.txt
```

## Шаг 10. Размер каждого файла в ~/boost-libs

Файл: step10_sizes.txt

Команда:
```sh
du -h ~/boost-libs/* | tee step10_sizes.txt
```

## Шаг 11. Топ-10 самых больших файлов

Файл: step11_top10.txt

Команда:
```sh
du -h ~/boost-libs/* | sort -hr | head -n 10 | tee step11_top10.txt
```
