//https://replit.com/@vivia25/Chatbot-Lab-Gold#Main.java

import java.util.Scanner;

//import org.graalvm.compiler.replacements.SnippetTemplate.UsageReplacer;

public class Main {

  public static void main(String[] args) {
    Scanner sc = new Scanner(System.in);
    System.out.println("Hi there.  What's up with you today? If you can't talk, just type \"bye<Enter>\"");
    String userResponse = sc.nextLine();
    while (!userResponse.equals("bye")) {
      System.out.println(getResponse(userResponse));
      userResponse = sc.nextLine();
    }
    System.out.println("It was nice talking to you!");
  }

  /**CRISTINA, NICK, BEVAN, RODANTE
   * Search for the substring word in response and return the index of its
   * first occurrence, returning -1 if it does not occur in userResp. This method
   * has similar functionality as indexOf String method, except that it only
   * returns a location for the word if either the word is the first or last word
   * user's response or a word with spaces on either side of it within the user's
   * response. indexOf would find the word even if it was a part of another word.
   */
  private static int findKeyword(String word, String response) 
  {
    if (response.indexOf(" " + word + " ")!=-1)
      return response.indexOf(" " + word + " ")+1;
    else if (response.indexOf(word+" ")==0)
      return response.indexOf(word + " ");  
    else if (response.indexOf(" "+word)!=-1)
      return response.indexOf(" " + word)+1;
    else 
      return -1;     
  }

  /** VIVIAN, VINAY, LUCAS, LAUREN, RAPHAEL
	 * Generate a random int value with 5 values.  int num=(int)(Math.random()*5)+1
	 * Based on the value, return 1 of 4 canned responses that prompt 
   * user to talk about their family, the weather, school, the election, or the pandemic
	 * To generate random int between and including 0 and 3
	 * int num=(int) (Math.random()*4)
	 */
	private static String getRandomResponse()
	{
   int num=(int)(Math.random()*5)+1;
   if (num==1)
    return("How is your family?");
    else if (num==2)
      return ("How is the weather?");
    else if (num==3)
      return"Are there windows in your school?";  //Ha!
    else if (num==4)
      return("Who won the election? ");
    else
      return("Is the pandemic over?"); 
	}


  /*
   * Based on the user's input String userResp, generate the chatbot's and return
   * it.
   */
  public static String getResponse(String userResp)
	{

    //Remove spaces at beginning and end of response.
	  userResp=userResp.trim();
	  userResp=userResp.toLowerCase();
    //remove punctuationi at end of response if it exists
	  if (userResp.substring(userResp.length()-1).equals(".")||
	      userResp.substring(userResp.length()-1).equals("?")||
	      userResp.substring(userResp.length()-1).equals("!"))
	  {
	      userResp=userResp.substring(0,userResp.length()-1);
	  }

    /*VIVIAN:
     *check for the word "no" as the FIRST word of the user's response and     *respond appropriately.
     */
	  if (findKeyword("no", userResp)!=-1)
	  {
	    return "You are wrong";
	  }

    /*VINAY:
     *check for the word "yes" as the FIRST word of the user's response and
     *respond appropriately.
     */   
	  else if (findKeyword("yes", userResp)==0)
	  {
      return "You are correct";
	  }

    /*LUCAS:
     *check for reference to the word "mother", "father", "sister",  "brother", 
     *and/or other family members respond appropriately
     */
    else if (findKeyword("mother", userResp)==0 || findKeyword("father", userResp)==0 || findKeyword("sister", userResp)==0 || findKeyword("brother", userResp)==0)
    {
      return "Family is important";
    }
    
    /*CRISTINA:
     *check for reference to the words "weather", "sunny", "rain",  "cloudy", of "snow"
     *and/or other weather related words and respond appropriately
     */
    else if (findKeyword("weather", userResp)==0 || findKeyword("sunny", userResp)==0 || findKeyword("rain", userResp)==0 || findKeyword("cloudy", userResp)==0 || findKeyword("snow",userResp)==0)
    {
      return "The weather is crazy";
    }


    /*NICK:
     *check for reference to the words "vote", "voted", "president", "Biden", "democrat", "republican 
     *and/or other election related words and respond appropriately
     */
    else if (findKeyword("vote", userResp)==0 || findKeyword("voted", userResp)==0 || findKeyword("president", userResp)==0 || findKeyword("biden", userResp)==0 || findKeyword("trump", userResp)==0 || findKeyword("democrat", userResp)==0 || findKeyword("republican", userResp)==0)
    {
      return "Aren't politics just the best?";
    }

    /*LAUREN:
     *check for reference to the words "school", "cohort", "class",  "schedule",  "virtual"
     *and/or other school related words and respond appropriately
     */
    else if (findKeyword("school", userResp)==0 || findKeyword("class", userResp)==0 || findKeyword("virtual", userResp)==0 || findKeyword("math", userResp)==0 ||findKeyword("science", userResp)==0 || findKeyword("history", userResp)==0 || findKeyword("english", userResp)==0)
    {
      return "School was a good time.";
    }

    /*VINAY:
     *check for reference to the words "covid", "pandemic", "vaccine", 
     *and/or other covid pandemic related words and respond appropriately
     */
    else if (findKeyword("covid",userResp)!=-1 ||
    findKeyword("pandemic",userResp)!=-1 || findKeyword ("vaccine",userResp)!=-1 )
    {
      return "Hopefully things will get better";
    }

   
    /*BEVAN:
     *check for the pattern "I want to ..." and response in a way that references "..." 
     *word for word as it appears in their response
     */
     else if (findKeyword("I want to", userResp)!=-1)
    {
      return "Why do you want to " + userResp.substring(10);
    }
   
    /*RAPHAEL:
     *check for the pattern "I like ..." and respond in a way that references "..."
     *word for word as it appears in their response
     */
     else if (findKeyword("I like", userResp)!=-1)
    {
      return "Why do you like" + userResp.substring(7);
    }
    
    /*LUCAS AND NICK:
     *check for the pattern "I am ..." and respond in a way that references ...
     *word for word as it appears in their response
     */
    else if (findKeyword("I am", userResp)!=-1)   //so the ... occurs at the 6th character after "I am"
    {
      return "Why are you " + userResp.substring(4) ;
    } 

     /*CRISTINA AND VIVIAN:
     *check for the pattern "I ... you" and respond in a way that references ...
     *word for word as it appears in their response
     */
    else if (findKeyword("i",userResp)!=-1 && findKeyword("you",userResp)>findKeyword("i",userResp)+3) //for this you can check to see if the indexOf "you" is greater than the indexOf "I"
    {
      return "Why do you "+userResp.substring(findKeyword("i",userResp)+2,findKeyword("you",userResp)-1)   +" me?";
    } 


    

    /*LAUREN AND RAPHAEL
     *check for the pattern "Do you ..." and respond in a way that references ...
     */  
    else if (findKeyword("Do you" , userResp+6)!=-1)  //so the response might be Yes I ....?"
    {
      return "Yes I " + userResp + ".";   //the ... will be 7 characters after the 
    } 
    
    /*RODANTE,  VINAY, AND BEVAN:
     *check for the pattern "It ... me" and respond in a way that references ...
      *You'll want to remove any s from any verb in ...
      */
    else if (findKeyword("it",userResp)!=-1 && findKeyword("me", userResp)>findKeyword("it",userResp)+3)
    {
      return "Why does " + userResp.substring(findKeyword("it",userResp),findKeyword("me",userResp)-1)+" you?";
    } 
  
    else
		{
      return getRandomResponse();
      
    }

	}

  
}
