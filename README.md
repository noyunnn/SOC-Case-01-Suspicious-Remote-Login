# SOC-Case-01-Suspicious-Remote-Login
## Project Overvie
Markdown
This project presents a simulated SOC investigation of suspicious remote login activity in a Windows environment.
The investigation focuses on analyzing Windows Security Events, identifying unusual authentication patterns, reviewing process activity, and assessing potential account compromise.
All data used in this project is fictional and created for educational purposes.

В этом проекте представлено имитационное SOC-расследование подозрительных действий при удаленном входе в систему в среде Windows. 
 Расследование сосредоточено на анализе событий безопасности Windows, выявлении необычных способов аутентификации, анализе активности процессов и оценке вероятности компрометации учетных записей. 
 Все данные, использованные в этом проекте, являются вымышленными и созданы в образовательных целях.
## Investigation Objective
The objective of this investigation is to:
- Analyze repeated failed login attempts followed by a successful remote logon.
- Identify the source workstation and the account involved.
- Examine Windows Security Events related to authentication and process creation.
- Review access to sensitive financial files.
- Determine whether the available evidence indicates suspicious activity or potential account compromise.
  
- Цель этого расследования состоит в том, чтобы:
- проанализировать повторяющиеся неудачные попытки входа в систему, за которыми следовал успешный удаленный вход.
- определить исходную рабочую станцию и учетную запись.
- изучить события безопасности Windows, связанные с аутентификацией и созданием процессов.
- проанализировать доступ к конфиденциальным финансовым файлам.
- определить, указывают ли имеющиеся доказательства на подозрительную активность или потенциальную компрометацию учетной записи.
## Incident Summary
- **Incident date:** 18 November 2026
- **Source workstation:** WS-022
- **Source IP:** 10.10.5.23
- **Target workstation:** WS-014
- **Account:** m.ivanova
- **Logon type:** 10 — Remote Interactive
- **Main concern:** Suspicious remote authentication and access to a sensitive financial file.
- **All activity is based on simulated training data**.
  
В ходе анализа журналов безопасности Windows была обнаружена серия неудачных попыток входа в систему, после которых произошла успешная удалённая авторизация.
Подключение было выполнено с рабочей станции **WS-022** **(IP-адрес: 10.10.5.23)** к рабочей станции **WS-014** с использованием учётной записи **m.ivanova**.
После успешной авторизации были зафиксированы запуск **PowerShell и CMD**, а также обращение к сетевой папке **Finance**, содержащей финансовые документы.
Дополнительный анализ показал, что под данной учётной записью был зафиксирован доступ на чтение файла **Payroll/November.xlsx.**

**Вся деятельность основана на смоделированных обучающих данных**.
## Tools and Technologies

- **Windows OS** — операционная система, события которой рассматриваются в учебном кейсе.
- **Windows Security Logs** — журналы безопасности Windows, содержащие информацию об авторизации и действиях пользователей.
- **Windows Event IDs** — идентификаторы событий, использованные для анализа.
- **Event Viewer** — инструмент Windows для просмотра системных журналов (изучается в рамках обучения).
- **PowerShell** — командная оболочка Windows, планируемая к практическому использованию для анализа событий.
- **GitHub** — платформа для хранения и публикации проекта.
  
### Technical Skills

- Анализ событий аутентификации.
- Построение хронологии инцидента (Event Timeline).
- Анализ удалённых подключений (Remote Logon Analysis).
- Анализ активности процессов (Process Activity).
- Анализ доступа к файлам и сетевым ресурсам.
- Оценка потенциальных рисков информационной безопасности.
- Подготовка отчётов по результатам расследования.

## Key Findings
1. **Repeated Failed Logons (Event ID 4625)**

   Зафиксировано пять неудачных попыток входа с IP-адреса 10.10.5.23.

2. **Successful Remote Logon (Event ID 4624)**

   После неудачных попыток произошла успешная удалённая авторизация под учётной записью m.ivanova на рабочей станции WS-014.

3. **Special Privileges Assigned (Event ID 4672)**

   Для сессии был зарегистрирован факт назначения специальных привилегий. Само по себе это событие не доказывает повышение привилегий пользователем.

4. **Process Creation (Event ID 4688)**

   После авторизации были зарегистрированы процессы powershell.exe и cmd.exe. Для определения их назначения необходим дополнительный анализ командных строк и родительских процессов.

5. **Network Share Access (Event ID 5140)**

   Зафиксировано обращение к сетевой папке Finance.

6. **File Read Access (Event IDs 5145 and 4663)**

   Зарегистрирован доступ на чтение файла Payroll/November.xlsx под учётной записью m.ivanova.

7. **Access Permissions**

   Согласно предоставленным данным, учётная запись m.ivanova имеет разрешение на чтение, но не имеет разрешений на запись и изменение указанного файла.

### Confirmed Facts and Limitations

- Установлена последовательность неудачных и успешной попыток авторизации.
- Установлены исходная и целевая рабочие станции.
- Подтверждён зарегистрированный доступ на чтение конкретного файла.
- Не установлено, кто физически выполнял действия.
- Не подтверждено изменение или удаление финансовых документов.
- Не установлена передача данных за пределы организации.
## Conclusion
По результатам анализа выявлена подозрительная последовательность событий: пять неудачных попыток авторизации, успешный удалённый вход под учётной записью m.ivanova, запуск командных оболочек Windows и последующий доступ на чтение финансового файла.

Совокупность этих событий требует дополнительной проверки, поскольку удалённая авторизация была выполнена с рабочей станции системного администратора с использованием учётной записи сотрудника бухгалтерии.

**Предварительный уровень риска: High (высокий приоритет дальнейшего расследования).**

При этом имеющиеся данные не подтверждают изменение финансовых документов, утечку информации или личность человека, совершившего действия.

Рекомендуется продолжить расследование:
- Проверить рабочую станцию WS-022.
- Установить, было ли удалённое подключение согласовано.
- Изучить полные командные строки запущенных процессов.
- Проверить дополнительные события безопасности и активность учётной записи.
- Передать результаты специалисту SOC L2 для дальнейшего анализа.

### Final Assessment

The available evidence indicates suspicious remote authentication and access to a sensitive financial file. Further investigation is required to determine the cause and scope of the activity.
