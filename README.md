# qa-final-project-java

Tema3

\[!\[CI/CD Pipeline](https://github.com/MihalacheCatalin/qa-final-project-java/actions/workflows/ci.yml/badge.svg)](https://github.com/MihalacheCatalin/qa-final-project-java/actions/workflows/ci.yml)





Detalii proiect : ce ar trebui sa faca, cum se ruleaza local etc (intr-un cadru ideal)

1. Fluxul Local (Dezvoltare)

Maven (mvn test): Deși nu este cod Java scris încă, Maven scanează folderul src/test/java. El caută fișiere care se termină în \*Test.java. Deoarece găsește doar un fișier .txt, va raporta "Build Success" cu 0 teste rulate. Acesta este comportamentul dorit pentru a valida structura.

Docker: Când rulezi docker build, Docker ia fișierul Dockerfile, instalează dependințele Maven în interiorul unei imagini izolate (container) și pregătește mediul să ruleze oriunde la fel.

2\. Fluxul CI/CD (GitHub Actions)

Imediat ce dai git push origin main, se declanșează automat fișierul ci.yml:

Job-ul de Test:

GitHub pornește o mașină virtuală curată.

Instalează Java 17.

Rulează mvn test. Dacă această comandă eșuează (de exemplu, dacă ai o eroare de sintaxă în pom.xml), pipeline-ul se oprește aici.

Job-ul de Build-and-Push:

Condiție: Rulează doar dacă job-ul de test a fost "Verde".

Autentificare: Se loghează pe Docker Hub folosind acele "Secrets" (parole ascunse) setate de tine.

Publicare: Construiește imaginea Docker și o urcă în repository-ul tău public de pe Docker Hub, unde poate fi descărcată de oricine pentru testare.

3\. Rolul fișierelor de configurare

app.yaml: În proiectele reale, codul tău va citi acest fișier pentru a ști la ce adresă să trimită request-urile (URL-ul de test). Este o metodă de a nu "hardcodat" datele sensibile direct în cod.

README.md: Badge-ul de sus se actualizează automat. Dacă pipeline-ul pică, badge-ul va deveni roșu (failing), oferind vizibilitate imediată asupra stării proiectului.





