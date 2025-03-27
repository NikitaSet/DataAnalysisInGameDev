# АНАЛИЗ ДАННЫХ [in GameDev]
Отчет по лабораторной работе #1 выполнил:
- Колотов Никита Александрович
- РИ230941
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | *| 20 |
| Задание 3 | * | 20 |

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

## Цель работы
освоить использование гугл-таблиц в проекте unity, освоить подключение звуковых файлов.

## Задание 1
Описать игровую переменную – здоровье, в игре СПАСТИ РТФ: Выживание.

Игровая роль:
1.	Демонстрирует сколько ударов может вынести игрок до поражения.
2.	Определяет выживаемость игрока: чем выше здоровье, тем дольше игрок способен выдерживать атаки зомби.
3.	Зомби наносят урон, уменьшая здоровье игрока.
4.	Влияет на регенерацию: если игрок не получает урона в течение определенного времени, его здоровье будет постепенно восстанавливатьс.
5.	Вампиризм позволяет игроку восстановить процент здоровья при нанесении урона по зомби, создавая цикл самоподдержания.
Условия изменения:
1.	Уменьшение:
-	При получении урона от зомби (величина урона зависит от силы зомби).
2.	Увеличение:
-	Регенерация: Медленное восстановление здоровья с течением времени, при отсутствии получаемого урона от зомби.
-	Вампиризм: Восстанавливает процент от наносимого урона здоровья за каждый удар по зомби.
-	Повышение уровня: Игрок модет прокачать свое максимальное здоровье, увеличивая его максимальное количество.
Допустимые значение:
-	Минимальное: 0 (смерть).
-	Максимальное: Зависит от максимального уровня прокачки игрока (Базовое значение – 30; С каждой прокачкой увеличивается на 10).

![image](https://github.com/user-attachments/assets/12bc9b26-86f9-427e-b878-ea06f40ae108)



## Задание 2
С помощью скрипта на языке Python заполните google-таблицу данными, описывающими выбранную игровую переменную в игре “СПАСТИ РТФ: Выживание”.

Код программы:
![image](https://github.com/user-attachments/assets/fd581625-9283-4e62-b620-67cf99d5162d)
![image](https://github.com/user-attachments/assets/07a51973-09b6-4514-a00a-4d9afe183b32)





## Задание 3
Настройте на сцене Unity воспроизведение звуковых файлов, описывающих динамику изменения выбранной переменной. Например, если выбрано здоровье главного персонажа вы можете выводить сообщения, связанные с его состоянием.

using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Health : MonoBehaviour
{
    public AudioSource healthSource; 
    public AudioClip damageSound;
    public AudioClip deathSound;

    private int maxHealth;
    private int currentHealth;

    private List<int> hpList = new List<int>() { 30, 20, 10, 0, 30 }; // Примерные значения хп
    private int currentHpIndex = 0; 
    private float nextSoundTime = 0f; 
    // Start is called before the first frame update
    void Start()
    {
        maxHealth = 30;
        currentHealth = maxHealth;
        healthSource = GetComponent<AudioSource>(); 
    }

    // Update is called once per frame
    void Update()
    {
        if (currentHpIndex < hpList.Count)
        {
            currentHealth = hpList[currentHpIndex]; 

            if (Time.time >= nextSoundTime)
            {
                if (currentHealth == maxHealth)
                {
                    healthSource.PlayOneShot(fullHealthSound);
                }
                else if (currentHealth > 0)
                {
                    healthSource.PlayOneShot(damageSound);
                }
                else if (currentHealth == 0)
                {
                    healthSource.PlayOneShot(deathSound);
                }

                nextSoundTime = Time.time + 5f; 
                currentHpIndex++; 
            }
        }
    }
}


## Выводы
Научились заполнять гугл-таблицу с помощью кода, подключать их к проекту unity, подключать туда же звуковые файлы.

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
