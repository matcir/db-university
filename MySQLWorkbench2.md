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
