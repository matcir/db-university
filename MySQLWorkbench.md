1.  Selezionare tutti gli studenti nati nel 1990 (160)

    SELECT \*
    FROM `students`
    WHERE YEAR(`date_of_birth`) = 1990;

2.  Selezionare tutti i corsi che valgono più di 10 crediti (479)

    SELECT \*
    FROM `courses`
    WHERE `cfu` > 10

3.  Selezionare tutti gli studenti che hanno più di 30 anni

    -Soluzione 1

         SELECT \*
         FROM `students`
         WHERE (YEAR(CURDATE()) - YEAR(`date_of_birth`) > 30)
         OR
         (YEAR(CURDATE()) - YEAR(`date_of_birth`) = 30
         AND
         MONTH(CURDATE()) > MONTH(`date_of_birth`)
         OR
         MONTH(CURDATE()) = MONTH(`date_of_birth`)
         AND
         DAY(CURDATE()) >= DAY(`date_of_birth`));

    -Soluzioe 2

         SELECT *
         FROM `students`
         WHERE TIMESTAMPDIFF(YEAR, `date_of_birth`, CURDATE()) > 30

4.  Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
    laurea (286)

    SELECT \*
    FROM `courses`
    WHERE `year` = 1 AND `period` = 'I semestre';

5.  Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
    20/06/2020 (21)

    SELECT \*
    FROM `exams`
    WHERE HOUR(`hour`) >= 14 AND `date` = "2020/06/20";

6.  Selezionare tutti i corsi di laurea magistrale (38)

    SELECT \*
    FROM `degrees`
    WHERE `level` = "magistrale";

7.  Da quanti dipartimenti è composta l'università? (12)

    SELECT COUNT(\*)
    FROM `departments`;

8.  Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

    SELECT COUNT(\*)
    FROM `teachers`
    WHERE `phone` IS NULL;
