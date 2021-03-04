# Day 1 BlogProject

## Review the Home work for SQL
 [SQL Link](https://sqliteonline.com/)

1. SELECT everything from a table
```sql
SELECT * FROM albums;
```

2. SELECT exactly one column from a table.
	SELECT more than one but not all columns from a table.
```sql
SELECT title FROM albums;
```

3. SELECT everything from the albums table whose id numbers are even and greater than 50,

	or odd and less than ten.
```sql
SELECT * FROM albums
  Where (albumid < 10 AND albumid % 2 != 0) OR (albumid > 50 AND albumid % 2 = 0)
;
```

```diff
+ Inform students that the order in which the `WHERE` commands are given
+ will determine the out put of the commands when it comes time to view.
+ In this case, the order was presented as such for easy viewing in the 
+ resulting output. 
```

4. INSERT ten new records into the playlists table.
```sql
INSERT Into playlists
 (Name)
VALUES
 ('MyPlaylist1'),
 ('MyPlaylist2'),
 ('MyPlaylist3'),
 ('MyPlaylist4'),
 ('MyPlaylist5'),
 ('MyPlaylist6'),
 ('MyPlaylist7'),
 ('MyPlaylist8'),
 ('MyPlaylist9'),
 ('MyPlaylist10');


```diff
+ This is how you can quickly enter in numerous new records at once
+ Also not no entry was needed for the `PlaylistId` due to the fact
+ that it is an Auto generated Primary Key.
```

5. Add an additional `DATETIME` column to the table named UpdatedAt. UPDATE artists with the third and fourth `ArtistId` to have a new `Name`.

	Before you UPDATE, do not forget to put CURRENT_TIMESTAMP into UpdatedAt. 
```sql
ALTER TABLE artists 
ADD COLUMN UpdatedAt DATETIME;
```
```sql
UPDATE artists
	Set Name = 'this is the third artist', UpdatedAt = CURRENT_TIMESTAMP
    WHERE ArtistId = 3;
```
```sql
UPDATE artists
	Set Name = 'this is the fourth artist', UpdatedAt = CURRENT_TIMESTAMP
    WHERE ArtistId = 4;
```
6. Use a TRANSACTION/ROLLBACK window to DELETE everything from the invoices table.
```sql
BEGIN TRANSACTION;
```
```sql
DELETE FROM invoices;
```
```sql
SELECT * FROM invoices;
```
```sql
ROLLBACK;
```
```sql
SELECT * FROM invoices;
```
7. Use a TRANSACTION/ROLLBACK window to DELETE everything from the albums table WHERE the AlbumID
	is odd, or even but greater than 8.
	Be sure to check to make sure the proper files were deleted. 
```sql
BEGIN TRANSACTION;
```
```sql
DELETE FROM albums
Where (albumid % 2 != 0) OR (albumid > 8 AND albumid % 2 = 0);
```
```sql
SELECT * FROM albums;
```
```sql
ROLLBACK;
```
```sql
SELECT * FROM albums;
```


## Begin Covering New Lesson

1. Brief Overview of past Concepts 
	- Slide 1

2. What we will be working with 
	- Slide 2

3. Start New STS starter project
	- `(Slide 5)` Project Naming
		- Name: TechTalentBlog
		- Group: com.tts
		- Desctiption: Blog Project for TTS
		- Package Name: com.tts.TechTalentBlog
	-`(Slide 6)` Dependencies to add
		- Spring Boot DevTools
		- Spring Data JPA
		- H2 Database
		- Spring Web Starter
		- ThymeLeaf

4. `(Slide 7)` Modify Application Properties
```java
spring.h2.console.enabled=true
spring.h2.console.path=/console
spring.datasource.platform=h2 
```

```diff
+ (Review)
+ The application properties allows to add addition configuration to our application.
+ Sort and sweet explination of individual properties.
```


```diff
-- The next step is to build the Stucture for our project!! --
```
5. Create Application Structure
	- Create Packages and classes
		- `(Slide 9)` Package Name: com.tts.TechTalentBlog.BlogPost
			- `(Slide 10)` Class Name: BlogPost
			- `(Slide 19)` Class Name: BlogPostController
			- `(Slide 31)` Interface Name: BlogPostRepository

	- In Templates
		- `(Slide 23)`Folder Name: blogpost
			- `(Slide 24)` File Name: index.html
			- `(Slide 35)` File Name: result.html


6. Adding the Actual Code
	- `(Slides 11 - 18)` BlogPost Code
		- Add the Class Level Tag
```java
@Entity
public class BlogPost {
```
		- Add our Field level Attributes`(Hand Written)`
```java
 // Who Can tell me why we Add the variables at the field level?
    @Id
    @GeneratedValue(strategy=GenerationType.AUTO)
    private Long id;
    private String title;
    private String author;
    private String blogEntry;
```
		- Add Generic Constructor `(Auto-Generate)`
```java
 // Why do we always have to add the Empty Constuctor in the Entity?
 public BlogPost(){}
```
		- Add Constructor with values `(Auto-Generate)`
```java
// What does this do? What value am I leaving out a value and Why?
public BlogPost(String title, String author, String blogEntry) {
	this.title = title; 
	this.author = author;
	this.blogEntry = blogEntry;
    }
```
		- Add Getters And Setters Leave out setId() `(Auto-Generate)`
```Java
//What are the getters and setters used for?
public Long getId(){
	return id;
}
public String getTitle(){
		return title;
}
public void setTitle(String title) {
	this.title = title;
}
public String getAuthor() {
	return author;
}
public void setAuthor(String author) {
	this.author = author;
}
public String getBlogEntry() {
	return blogEntry;
}
public void setBlogEntry(String blogEntry) {
	this.blogEntry = blogEntry;
}
```
		- Add toString() `(Auto-Generate)`
```java
@Override
public String toString() {
	return "BlogPost [id=" + id + ", title=" + title + ", author=" + author + ", blogEntry=" + blogEntry + "]";
}
```
		- Organize Imports `(CTRL + SHIFT + O)`
```java
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
```
		- Be sure you have saved your file `(CTRL + SHIFT + S)`

	- `(Slides 21 & 22)` BlogPostController Code
		- Add the @Conroller Annotation
```java
//This will help send the output to a template, not write output directly from the controller. 
@Controller
public class BlogPostController {
```
		- Add method for default path
```java
//causes the default localhost:8080 to go to the template returned by the following method
 @GetMapping(value="/")
	public String index(BlogPost blogPost) {
		return "blogpost/index";
	}
```
		- Be sure you have saved your file `(CTRL + SHIFT + S)`
	- `(Slides 25 - 27)` Let's take a minute to test out the code that we have written
		- Write some test code in our index.html
```html
<!DOCTYPE html>
<html>
  <head>
    <title>Blog Site</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>
  </head>
  <body>
    <h1>Welcome to Our Blog Post Site!</h1>
    <h3>Check out our blogs!</h3>
  </body>
</html>
```
		- Be sure you have saved your file `(CTRL + SHIFT + S)`
		- Right click project Run as Spring Boot Project
		- Run [localhost:8080/](http://localhost:8080/)
		- check for error here. Possible Errors Check the Following
			- ensure that files have all been saved
			- make sure they are running right project
			- ensure files have no errors
			- value passed to Controller Get Mapping
			- initial get mapping return
			- templates folder name
			- check dependancies
			- check to ensure pom file is correct
			- check spelling of all in index method and html
			- other fixes
				- clean file
				- update maven dependancies
				- close out completely
				- remove and then re-add tymeleaf
	- Update index.html
		- `(Slide 29)` Add in the link to the top html tab.`(Hand Write)`
```html
<html xmlns:th="http://www.thymeleaf.org">
```
		- `(Slide 30)` Add The Form to accept the object at the end of your body`(Hand Write)`
```html
<-- Why would we add a form in out HTML? --!>
<p>Please use the form below to submit a Blog Post:</p>
<form action="#" th:action="@{/}" th:object="${blogPost}" method="post">
    <table>
	<tr>
            <td>Title</td>
	    <td><input type="text" th:field="*{title}" /></td>
	</tr>
	<tr>
	    <td>Author:</td>
	    <td><input type="text" th:field="*{author}" /></td>
	</tr>
	<tr>
    	    <td>Blog Entry:</td>
	    <td><input type="text" th:field="*{blogEntry}" /></td>
	</tr>
	<tr>
	    <td><button type="submit">Submit Your Post</button></td>
	</tr>
    </table>
</form>
```
	- `(Slide 33)` Update the Interface
```java
// We add this add and update this interface because it allows us to post the form to our database
// So in order for this to communicate with out Thyme
package com.techtalentsouth.TechTalentBlog.BlogPosts;
import org.springframework.data.repository.CrudRepository;
public interface BlogPostRepository extends CrudRepository<BlogPost, Long>{
}
```
	- `(Slide 34)` Updating our controller to handle the new Functionality and work with the database
```java
//Add this right under the class
//This injects our blog repository when our class is called.
@Autowired
private BlogPostRepository blogPostRepository;
//add this underneath the index()
 private BlogPost blogPost;  
 @PostMapping(value = "/")
 public String addNewBlogPost(BlogPost blogPost, Model model) {
	blogPostRepository.save(new BlogPost(blogPost.getTitle(), blogPost.getAuthor(), blogPost.getBlogEntry()));
	model.addAttribute("title", blogPost.getTitle());
	model.addAttribute("author", blogPost.getAuthor());
	model.addAttribute("blogEntry", blogPost.getBlogEntry());
	return "blogpost/result";
  }
 //hint it copy and pasting use (CTRL + SHIFT + F)
```
	- `(Slide 36)` Update our result.html To handle out Postmapping
```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <head>
    <title>Blog Site</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
  </head>
  <body>
    <h3>Blog Post Form</h3>
    <p>Thank you for your submission!</p>
    <h4>Blog Post:</h4>
    <p th:text="${title}" />
    <p th:text="${author}" />
    <p th:text="${blogEntry}" />
  </body>
</html>
```
7. `(Slides 37 - 42)`Test the Final project for today
	- Ensure that everything is saved
	- Check for any errors in the file and fix them.
	- Run the application -make sure it is the correct one-
	- Open [localhost:8080/](http://localhost:8080/)
	- Fill out the form on the page
	- View the results on the result.html
	- Check /console
	- Copy the value from STS console into the DB console
	- Select all from the table by double clicking it. 
	- Run and ensure the result was added to the DB
	- trouble shoot Quick Issues

8. Tomorrow we will
	- Make the forms and site prettier by bringing in Bootstrap
	- Bring in a Navbar 
	- Give us options to Edit & Destroy
9. NO HOME WORK
	- Further Trouble shooting 
10. Post to the Notes and Survey to Slack
	- [Google Sheets New/Review Concepts](https://docs.google.com/document/d/1NMlLE6IERw2yyvPVEYo10TcqESsMNq1chKJ828sBEkQ/edit?usp=sharing)
	- [Post Class Survey](https://PollEv.com/surveys/9G5UYdxkeygqc52YAlyIM/respond)
	- Be Sure to download and Remove the previous day's results with a picture of the emotion chart
