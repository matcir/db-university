GROUP BY QUERIES:

1.  Contare quanti iscritti ci sono stati ogni anno

    SELECT COUNT(\*) as `total_students`,
    YEAR(`enrolment_date`) as `year`
    FROM `students`
    GROUP BY `year`;

2.  Contare gli insegnanti che hanno l'ufficio nello stesso edificio

    SELECT COUNT(\*) AS `number_of_teachers`,
    `office_address`
    FROM `teachers`
    GROUP BY `office_address`;

3.  Calcolare la media dei voti di ogni appello d'esame

    SELECT `exam_id` AS `exam`,
    AVG(`vote`) AS `average_vote`
    FROM `exam_student`
    GROUP BY `exam`;

4.  Contare quanti corsi di laurea ci sono per ogni dipartimento

    SELECT COUNT(\*) AS `number of degrees`,
    `department_id` AS `department`
    FROM `degrees`
    GROUP BY `department`

JOIN QUERIES:

1.  Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

    SELECT `students`.`name`,
    `students`.`surname`,
    `students`.`email`,
    `students`.`enrolment_date`,
    `degrees`.`name` as `degree`
    FROM `students`
    JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`
    WHERE `degrees`.`name` = "Corso di Laurea in Economia";

2.  Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

    SELECT `departments`.`name` AS `department`,
    `degrees`.`name`,
    `degrees`.`id`,
    `degrees`.`level`
    FROM `departments`
    JOIN `degrees` ON `degrees`.`department_id` = `departments`.`id`
    WHERE `departments`.`name` = "Dipartimento di Neuroscienze"
    AND `degrees`.`level` = "magistrale";

3.  Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

    SELECT `teachers`.`name`,
    `teachers`.`surname`,
    `courses`.`name`,
    `courses`.`description`,
    `courses`.`cfu`,
    `courses`.`id`
    FROM `teachers`
    JOIN `course_teacher` ON `course_teacher`.`teacher_id` = `teachers`.`id`
    JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id`
    WHERE `teachers`.`name` = "Fulvio"
    AND `teachers`.`surname` = "Amato";

4.  Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

    SELECT `students`.`name` AS `name`,
    `students`.`surname` AS `surname`,
    `students`.`registration_number` AS `registration_number`,
    `students`.`date_of_birth` AS `date_of_birth`,
    `departments`.`name` AS `department`,
    `departments`.`id` AS `department_id`,
    `departments`.`address` AS `department_address`,
    `departments`.`email` AS `department_email`,
    `degrees`.`id` AS `degree_id`,
    `degrees`.`name` AS `degree`,
    `degrees`.`level` AS `level`,
    `degrees`.`address` AS `degree_address`
    FROM `students`
    JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`
    JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`
    ORDER BY `students`.`surname`, `students`.`name`

5.  Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

    SELECT `degrees`.`name`,
    `teachers`.`name` AS `teacher name`,
    `teachers`.`surname` AS `teacher surname`,
    `courses`.`name` AS `course`,
    `courses`.`id`,
    `courses`.`description`
    FROM `degrees`
    JOIN `courses` ON `courses`.`degree_id` = `degrees`.`id`
    JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id`
    JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`

6.  Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

    SELECT `teachers`.\*
    FROM `departments`
    JOIN `degrees` ON `departments`.`id` = `degrees`.`department_id`
    JOIN `courses` ON `courses`.`degree_id` = `degrees`.`id`
    JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id`
    JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
    WHERE `departments`.`name` = "Dipartimento di Matematica"

7.  BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18

    SELECT `students`.`id`,
    `students`.`name`,
    `students`.`surname`,
    `students`.`registration_number`,
    `exams`.`id`,
    MAX(`exam_student`.`vote`) AS `highest vote`,
    COUNT(`exam_student`.`vote`) AS `attempts`
    FROM `students`
    JOIN `exam_student` ON `exam_student`.`student_id` = `students`.`id`
    JOIN `exams` ON `exam_student`.`exam_id` = `exams`.`id`
    GROUP BY `students`.`id`, `exams`.`id`;
