Here are the **Top 50 Spring Data JPA Interview Questions**, carefully selected and tailored for professionals with **3–5 years of experience**. These questions cover core concepts, advanced querying, repositories, auditing, projections, and real-world challenges.

---

## ✅ Top 50 Spring Data JPA Interview Questions (3–5 Years Experience)

---

### 🔹 **1–10: Core Spring Data JPA Concepts**

1. What is Spring Data JPA, and how does it relate to Hibernate and JPA?
2. What are the advantages of using Spring Data JPA in enterprise applications?
3. What is the role of the `@Entity` and `@Table` annotations?
4. How do you configure Spring Data JPA in a Spring Boot project?
5. What is the difference between JPA and Hibernate?
6. What is the role of `@Id` and `@GeneratedValue` in an entity?
7. What are the default fetching strategies in JPA for `@OneToMany` and `@ManyToOne`?
8. What is the difference between FetchType.LAZY and FetchType.EAGER?
9. How do you handle bi-directional relationships and prevent infinite recursion in JSON serialization?
10. What are common annotations used for defining entity relationships?

---

### 🔹 **11–20: Repositories & Derived Queries**

11. What is the difference between `CrudRepository`, `JpaRepository`, and `PagingAndSortingRepository`?
12. How does Spring Data generate queries from method names?
13. What are some examples of derived query method naming conventions?
14. How do you define custom queries using `@Query`?
15. What is the difference between JPQL and native SQL in Spring Data JPA?
16. How do you use `@Modifying` and `@Transactional` annotations in update/delete queries?
17. What is the purpose of the `flush()` method in JPA?
18. What are the advantages of using `Optional` as a return type in repository methods?
19. How do you implement pagination and sorting with `Pageable` and `Sort`?
20. How do you check for the existence of a record using repository methods?

---

### 🔹 **21–30: Advanced Querying & Projections**

21. What are projections in Spring Data JPA?
22. What is the difference between interface-based and class-based projections?
23. What is a DTO projection, and how is it implemented?
24. How do you fetch partial data using projections?
25. What is the use of `@EntityGraph` and how does it help avoid the N+1 problem?
26. What are Specifications in Spring Data JPA?
27. How do you build dynamic queries using the Specification API?
28. What is the Criteria API, and how is it different from JPQL?
29. What is Query By Example (QBE) in Spring Data?
30. How do you use `@QueryHints` for performance tuning?

---

### 🔹 **31–40: Auditing, Events & Soft Deletes**

31. How do you enable and configure auditing in Spring Boot with Spring Data JPA?
32. What is the role of `@CreatedDate`, `@LastModifiedDate`, and `AuditorAware`?
33. How do you implement entity listeners in JPA?
34. What are JPA lifecycle callbacks and annotations like `@PrePersist`, `@PostUpdate`, etc.?
35. How do you implement soft deletes in Spring Data?
36. What are `@SQLDelete` and `@Where` annotations used for?
37. How do you log or audit entity changes in a generic way?
38. What is an entity listener class and how is it registered?
39. What are the use cases for using `@Version` in entities?
40. How do you prevent concurrent updates in JPA?

---

### 🔹 **41–50: Best Practices, Optimization & Testing**

41. What are the common performance pitfalls with Spring Data JPA?
42. How do you avoid LazyInitializationException?
43. What are the benefits and caveats of using `@Transactional(readOnly = true)`?
44. How does first-level and second-level caching work in JPA?
45. What is the difference between `persist()`, `merge()`, `detach()`, and `refresh()`?
46. How do you optimize batch inserts/updates?
47. How do you implement unit tests for Spring Data repositories?
48. What is `@DataJpaTest` and how is it used?
49. How do you use TestContainers with Spring Data JPA?
50. When should you avoid using Spring Data JPA in enterprise applications?

---

Would you like the **answers and explanations** for these 50 questions next, along with **topic-wise deep dives**, **real-world use cases**, and **a downloadable PDF** version at the end?
