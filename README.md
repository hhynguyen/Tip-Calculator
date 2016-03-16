/*Fortune cookie fortunes were taken from Josh Madison's site at http://joshmadison.com/2008/04/20/fortune-cookie-fortunes/.
Background images were provided by various users from Stock.XCHNG at http://www.sxc.hu/.
*/

package archer.reference.tip;

import java.util.ArrayList;
import java.util.Collections;
import java.util.Random;

import android.os.Bundle;
import android.app.Activity;
import android.content.Intent;
import android.content.SharedPreferences;
import android.content.SharedPreferences.Editor;
import android.content.pm.ActivityInfo;
import android.text.InputFilter;
import android.view.Gravity;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.view.View.OnClickListener;
import android.view.View.OnFocusChangeListener;
import android.widget.Button;
import android.widget.EditText;
import android.widget.ImageButton;
import android.widget.ScrollView;
import android.widget.SeekBar;
import android.widget.SeekBar.OnSeekBarChangeListener;
import android.widget.TableLayout;
import android.widget.TableRow;
import android.widget.TextView;

public class MainActivity extends Activity implements OnClickListener, OnSeekBarChangeListener, OnFocusChangeListener{

	private SharedPreferences someData;
	private Editor editor;
	private static String filename = "jttSettings";
	private ScrollView bg;
	private InputFilter[] filter3 = new InputFilter[1];
	private InputFilter[] filter8 = new InputFilter[1];
	private InputFilter[] filter16 = new InputFilter[1];
	private boolean inBed = false;
	private boolean round = false;
	private boolean seek = true;
	private int tipPercentValue = 15;
	private double subTotal = 0.0;
	private double finalTotalBill = 0.0;
	private double totalTip = 0.0;
	private double roundTip = 0.0;
	private double totalTax = 0.0;
	private TextView grandTotalBox;
	private EditText tipPercentBox;
	private TextView tipDollarBox;
	private EditText taxDollarBox;
	private TextView fortuneTextBox;
	private SeekBar tipBar;
    private ArrayList<View> buttonList = new ArrayList<View>();
    private ArrayList<EditText> amountList = new ArrayList<EditText>();
    private ArrayList<EditText> nameList = new ArrayList<EditText>();
    private ArrayList<Diner> dinerList = new ArrayList<Diner>();
    private ArrayList<String> fortuneList = new ArrayList<String>();
    private int bgIndex = 0;
    
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        
        //saved stuff
        someData = getSharedPreferences(filename,0);
        editor = someData.edit();
        
        //make fortunes
        Collections.addAll(fortuneList,
        		"\'Welcome\' is a powerful word.", "A dubious friend may be an enemy in camouflage.","A feather in the hand is better than a bird in the air.","A fresh start will put you on your way.","A friend asks only for your time not your money.","A friend is a present you give yourself.","A gambler not only will lose what he has, but also will lose what he doesn�t have.","A golden egg of opportunity falls into your lap this month.","Now is a good time to finish up old tasks.","A hunch is creativity trying to tell you something.","A light heart carries you through all the hard times.","A new perspective will come with the new year.","A person is never too old to learn.","A person of words and not deeds is like a garden full of weeds.","A pleasant surprise is waiting for you.","A smile is your personal welcome mat.","A truly rich life contains love and art in abundance.","A soft voice may be awfully persuasive.","Accept something that you cannot change, and you will feel better.","Adventure can be real happiness.","Advice is like kissing. It costs nothing and is a pleasant thing to do.","Advice, when most needed, is least heeded.","All the effort you are making will ultimately pay off.","All the troubles you have will pass away very quickly.","All will go well with your new project.","All your hard work will soon pay off.","Allow compassion to guide your decisions.","An agreeable romance might begin to take on the appearance.","An important person will offer you support.","An inch of time is an inch of gold.","Be careful or you could fall for some tricks today.",
        		"Beauty in its various forms appeals to you.","Because you demand more from yourself, others respect you deeply.","Believe in yourself and others will too.","Believe it can be done.","Better ask twice than lose yourself once.",
        		"Carve your name on your heart and not on marble.","Change is happening in your life, so go with the flow!","Competence like yours is underrated.","Congratulations! You are on your way.","Could I get some directions to your heart?","Courtesy begins in the home.","Courtesy is contagious.","Curiosity kills boredom. Nothing can kill curiosity.",
        		"Dedicate yourself with a calm mind to the task at hand.","Depart not from the path which fate has you assigned.","Determination is what you need now.","Disbelief destroys the magic.","Distance yourself from the vain.","Do not be intimidated by the eloquence of others.","Do not let ambitions overshadow small success.","Do not make extra work for yourself.","Do not underestimate yourself. Human beings have unlimited potentials.","Don\'t be discouraged, because every wrong attempt discarded is another step forward.","Don\'t confuse recklessness with confidence.","Don\'t just spend time. Invest it.","Don\'t just think, act!","Don\'t let friends impose on you, work calmly and silently.","Don\'t let the past and useless detail choke your existence.","Don\'t let your limitations overshadow your talents.","Don\'t worry; prosperity will knock on your door soon.",
        		"Each day, compel yourself to do something you would rather not do.","Education is the ability to meet life\'s situations.","Emulate what you admire in your parents.","Emulate what you respect in your friends.","Every flower blooms in its own sweet time.","Every wise man started out by asking many questions.","Everyday in your life is a special occasion.",
        		"Failure is the chance to do better next time.","Feeding a cow with roses does not get extra appreciation.","For hate is never conquered by hate. Hate is conquered by love.","Fortune Not Found: Abort, Retry, Ignore?","From listening comes wisdom, and from speaking, repentance.","From now on your kindness will lead you to success.",
        		"Get your mind set - confidence will lead you on.","Go take a rest; you deserve it.","Good news will be brought to you by mail.","Good to begin well, better to end well.",
        		"Happiness begins with facing life with a smile and a wink.","Happiness will bring you good luck.","A happy life is just in front of you.","Hard words break no bones, fine words butter no parsnips.","Have a beautiful day.","He who expects no gratitude shall never be disappointed.","He who knows he has enough is rich.","Help! I\'m being forced to write fortunes against my will!","How you look depends on where you go.",
        		"I learn by going where I have to go.","If a true sense of value is to be yours it must come through service.","If certainty were truth, we would never be wrong.","If you continually give, you will continually have.","If you look in the right places, you can find some good offerings.","If you think you can do a thing or think you can\'t do a thing, you\'re right.","If your desires are not too extravagant, they will be granted.","In order to take, one must first give.","In the end all things will be known.","It could be better, but it\'s good enough.","It is better to deal with problems before they arise.","It is honorable to stand up for what is right, however unpopular it seems.","It is worth reviewing some old lessons.","It takes courage to admit fault.","It\'s time to get moving. Your spirits will lift accordingly.",
        		"Keep your face to the sunshine and you will never see shadows.",
        		"Let the world be filled with tranquility and goodwill.","Listen not to vain words of empty tongue.","Listen to everyone. Ideas come from everywhere.","Living with a commitment to excellence shall take you far.","Long life is in store for you.","Love is a warm fire to keep the soul warm.","Love is like sweet medicine, good to the last drop.","Love lights up the world.","Love truth, but pardon error.","Man is born to live and not prepared to live.","Many will travel to hear you speak.","Meditation with an old enemy is advised.","Miles are covered one step at a time.",
        		"Nature, time and patience are the three great physicians.","Never fear! The end of something marks the start of something new.","New ideas could be profitable.","New people will bring you new realizations, especially about big issues.","No one can walk backwards into the future.","Now is a good time to buy stock.","Now is the time to go ahead and pursue that love interest!","Now is the time to try something new.",
        		"Others can help you now.",
        		"Pennies from heaven find their way to your doorstep this year!","People are attracted by your delicate features.","People find it difficult to resist your persuasive manner.","Perhaps you\'ve been focusing too much on saving.","Physical activity will dramatically improve your outlook today.","Place special emphasis on old friendship.","Practice makes perfect.","Protective measures will prevent costly disasters.","Put your mind into planning today. Look into the future.","Remember to share good fortune as well as bad with your friends.","Rest has a peaceful effect on your physical and emotional health.","Resting well is as important as working hard.",
        		"Romance moves you in a new direction.",
        		"Savor your freedom - it is precious.","Say hello to others. You will have a happier day.","Self-knowledge is a life long process.","Share your joys and sorrows with your family.","Sloth makes all things difficult; industry all easy.","Small confidences mark the onset of a friendship.","Society prepares the crime; the criminal commits it.","Someone you care about seeks reconciliation.","Soon life will become more interesting.","Stand tall. Don\'t look down upon yourself.","Stop searching forever, happiness is just next to you.","Success is a journey, not a destination.","Success is going from failure to failure without loss of enthusiasm.",
        		"Take care and sensitivity you show towards others will return to you.","Take the high road.","The austerity you see around you covers the richness of life like a veil.","The best prediction of future is the past.","The change you started already has far-reaching effects. Be ready.","The first man gets the oyster, the second man gets the shell.","The harder you work, the luckier you get.","The night life is for you.","The one that recognizes the illusion does not act as if it is real.","The only people who never fail are those who never try.","The person who will not stand for something will fall for anything.","The philosophy of one century is the common sense of the next.","The saints are the sinners who keep on trying.","The secret to good friends is no secret to you.","The small courtesies sweeten life, the greater ennoble it.","The smart thing to do is to begin trusting your intuitions.","The strong person understands how to withstand substantial loss.","The sure way to predict the future is to invent it.","The truly generous share, even with the undeserving.","The value lies not within any particular thing, but in the desire placed on that thing.","The weather is wonderful.","There is no mistake so great as that of being always right.","There is no wisdom greater than kindness.","There is not greater pleasure than seeing your loved ones prosper.","There\'s no such thing as an ordinary cat.","Things don\'t just happen; they happen just.","Those who care will make the effort.","Time and patience are called for; many surprises await you!","Time is precious, but truth is more precious than time.","To know oneself, one should assert oneself.","Today, conserve yourself, as things just won/'t budge.","Today, your mouth might be moving but no one is listening.","Tonight you will be blinded by passion.",
        		"Use your eloquence where it will do the most good.",
        		"Welcome change.","Well done is better than well said.","What\'s hidden in an empty box?","What\'s yours in mine, and what\'s mine is mine.","When your heart is pure, your mind is clear.",
        		"You always bring others happiness.","You are a person of another time.","You are a talented storyteller.","You are admired by everyone for your talent and ability.","You are almost there.","You are busy, but you are happy.","You are generous to an extreme and always think of the other fellow.","You are going to have some new clothes.","You are in good hands this evening.","You are modest and courteous.","You are never selfish with your advice or your help.","You are next in line for promotion in your firm.","You are offered the dream of a lifetime. Say yes!","You are open-minded and quick to make new friends.","You are solid and dependable.","You are soon going to change your present line of work.","You are talented in many ways.","You are the master of every situation.","You are very expressive and positive in words, act and feeling.","You are working hard.","You begin to appreciate how important it is to share your personal beliefs.","You desire recognition and you will find it.","You have a deep appreciation of the arts and music.","You have a deep interest in all that is artistic.","You have a friendly heart and are well admired.","You have a shrewd knack for spotting insincerity.","You have a yearning for perfection.","You have an active mind and a keen imagination.","You have an ambitious nature and may make a name for yourself.","You have unusual equipment for success, use it properly.","You have exceeded what was expected.","You have the power to write your own fortune.","You have yearning for perfection.","You know where you are going and how to get there.","You look pretty.","You love challenge.","You love food.","You make people realize that there exist other beauties in the world.","You never hesitate to tackle the most difficult problems.","You seek to shield those you love.","You should be able to make money and hold on to it.","You should be able to undertake and complete anything.","You understand how to have fun with others and to enjoy your solitude.","You will always be surrounded by true friends.","You will always get what you want through your charm and personality.","You will always have good luck in your personal affairs.","You will be a great success both in the business world and society.","You will be blessed with longevity.","You will be successful in your work.","You will be traveling and coming into a fortune.","You will be unusually successful in business.","You will become a great philanthropist in your later years.","You will become more and more wealthy.","You will enjoy good health.","You will be surrounded by luxury.","You will find great contentment in the daily, routine activities.","You will have a fine capacity for the enjoyment of life.","You will have gold pieces by the bushel.","You will inherit a large sum of money.","You will make change for the better.","You will soon be surrounded by good friends and laughter.","You will take a chance in something in near future.","You will travel far and wide, both for pleasure and for business.","Your abilities are unparalleled.","Your ability is appreciated.","Your ability to juggle many tasks will take you far.","Your biggest virtue is your modesty.","Your character can be described as natural and unrestrained.","Your difficulties will strengthen you.","Your dreams are never silly; depend on them to guide you.","Your dreams are worth your best efforts to achieve them.","Your energy returns and you get things done.","Your family is young, gifted and attractive.","Your first love has never forgotten you.","Your happiness is before you, not behind you! Cherish it.","Your hard work will payoff today.","Your heart will always make itself known through your words.","Your home is the center of great love.","Your ideals are well within your reach.","Your infinite capacity for patience will be rewarded sooner or later.","Your leadership qualities will be tested and proven.","Your life will be happy and peaceful.","Your life will get more and more exciting.","Your love life will be happy and harmonious.","Your love of music will be an important part of your life.","Your loyalty is a virtue, but not when it\'s wedded with blind stubbornness.","Your mind is creative, original and alert.","Your mind is your greatest asset.","Your quick wits will get you out of a tough situation.","Your success will astonish everyone.","Your talents will be recognized and suitably rewarded.","Your work interests can capture the highest status and prestige.",
        		//wow shit
        		"You are not prepared!","BY FIRE BE PURGED!","Tempest Keep was merely a setback.","You no take candle!","Mmmrrrggglll!","In the mountains...","NO! NO! NO! NO! NO!","Frostmourne hungers...","BONE STORM!","TOO SOON!","TASTE THE FLAMES OF SULFURON!"
        		);
        
        //make filters
        filter3[0] = new InputFilter.LengthFilter(3);
        filter8[0] = new InputFilter.LengthFilter(8);
        filter16[0] = new InputFilter.LengthFilter(16);
        
        //get ids
        bg = (ScrollView)findViewById(R.id.bg);
        fortuneTextBox = (TextView)findViewById(R.id.fortuneTextBox);
        grandTotalBox = (TextView)findViewById(R.id.textGTotal2);
        tipPercentBox = (EditText)findViewById(R.id.tipPercent);
        tipDollarBox = (TextView)findViewById(R.id.tipDollar);
        taxDollarBox = (EditText)findViewById(R.id.taxDollar);
        tipBar = (SeekBar)findViewById(R.id.tipSlider);
        ImageButton ib = (ImageButton)findViewById(R.id.addDinerButton);
        EditText et1 = (EditText)findViewById(R.id.firstCustomer);
        EditText et2 = (EditText)findViewById(R.id.amount1of1);
        ImageButton ib2 = (ImageButton)findViewById(R.id.addButton1);
        TextView tv1 = (TextView)findViewById(R.id.textSplit1);
        TextView tv2 = (TextView)findViewById(R.id.textSplit1Dollar);
        ImageButton rb = (ImageButton)findViewById(R.id.roundButton);
        Button resetButton = (Button)findViewById(R.id.resetButton);
        ImageButton fortuneGen = (ImageButton)findViewById(R.id.fortuneButton);
        
        //set filters
        tipPercentBox.setFilters(filter3);
        taxDollarBox.setFilters(filter8);
        et1.setFilters(filter16);
        et2.setFilters(filter8);
        
        //create first diner
        Diner diner = new Diner(et1, et2, ib2, tv1, tv2, this);
        dinerList.add(diner);
        
        //set listeners
        tipPercentBox.setOnFocusChangeListener(this);
        taxDollarBox.setOnFocusChangeListener(this);
        tipBar.setOnSeekBarChangeListener(this);
        ib.setOnClickListener(this);
        rb.setOnClickListener(this);
        resetButton.setOnClickListener(this);
        fortuneGen.setOnClickListener(this);
        
        //add stuff to category lists
        buttonList.add(diner.button);
        amountList.add(et2);
        nameList.add(et1);
        

        
        //no screen orientation changes
        setRequestedOrientation (ActivityInfo.SCREEN_ORIENTATION_PORTRAIT);
        
        //load shit
        bgIndex = someData.getInt("bg", 0);
        getBg();
        round = someData.getBoolean("round", round);
        if (round)
        {
        	rb.setImageResource(R.drawable.exact);
        }
        tipPercentValue = someData.getInt("tip", 15);
        updateTip();
        inBed = someData.getBoolean("bed",false);
        if (inBed)
		{
			Random rand1 = new Random();
	        String tempFort = fortuneList.get(rand1.nextInt(fortuneList.size()));
	        tempFort = tempFort.substring(0,tempFort.length()-1)+" in bed.";
			fortuneTextBox.setText("\""+tempFort+"\"");
		}
		else
		{
			Random rand2 = new Random();
	        String tempFort = fortuneList.get(rand2.nextInt(fortuneList.size()));
			fortuneTextBox.setText("\""+tempFort+"\"");
		}
    }

    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        getMenuInflater().inflate(R.menu.activity_main, menu);
        return true;
    }
    
    @Override
    public boolean onOptionsItemSelected(MenuItem item)
    {
    	if (item.getItemId() == R.id.bgcolor)
    	{
    		bgIndex ++;
    		if (bgIndex >= 16)
    		{
    			bgIndex = 0;
    		}
    		editor.putInt("bg",bgIndex);
    		editor.commit();
    		getBg();
    	}
    	else if (item.getItemId() == R.id.fortunesmod)
    	{
    		
    		if (inBed)
    		{
    			inBed = false;
    			String tempString1 = fortuneTextBox.getText().toString();
    			tempString1 = (tempString1.substring(0,tempString1.length()-9))+".\"";
    			fortuneTextBox.setText(tempString1);
    			editor.putBoolean("bed",inBed);
    			editor.commit();
    			
    		}
    		else
    		{
    			inBed = true;
    			String tempString2 = fortuneTextBox.getText().toString();
    			tempString2 = tempString2.substring(0,tempString2.length()-2)+" in bed.\"";
    			fortuneTextBox.setText(tempString2);
    			editor.putBoolean("bed",inBed);
    			editor.commit();
    		}
    	}
    	return(super.onOptionsItemSelected(item));
    }

	public void onClick(View v) {
		if (v.getId()== R.id.fortuneButton)
		{
			if (inBed)
			{
				Random rand1 = new Random();
		        String tempFort = fortuneList.get(rand1.nextInt(fortuneList.size()));
		        tempFort = tempFort.substring(0,tempFort.length()-1)+" in bed.";
				fortuneTextBox.setText("\""+tempFort+"\"");
			}
			else
			{
				Random rand2 = new Random();
		        String tempFort = fortuneList.get(rand2.nextInt(fortuneList.size()));
				fortuneTextBox.setText("\""+tempFort+"\"");
			}
		}
		else if (v.getId() == R.id.resetButton)
		{
		    Intent intent = getIntent();
		    overridePendingTransition(0, 0);
		    intent.addFlags(Intent.FLAG_ACTIVITY_NO_ANIMATION);
		    finish();
		    overridePendingTransition(0, 0);
		    startActivity(intent);
		}
		else if (v.getId()==R.id.roundButton)
		{
			if (round)
			{
				((ImageButton) v).setImageResource(R.drawable.round);
				tipDollarBox.setText("$"+String.format("%,.02f", totalTip));
				finalTotalBill = subTotal+totalTip+totalTax;
				for (Diner diner : dinerList)
				{
					diner.updateFinalTotal(subTotal, totalTax, totalTip);
				}
				round = false;
				editor.putBoolean("round", round);
				editor.commit();
			}
			else
			{
				((ImageButton) v).setImageResource(R.drawable.exact);
				roundTip = Math.ceil(totalTip);
				tipDollarBox.setText("$"+String.format("%,.02f", roundTip));
				finalTotalBill = subTotal+roundTip+totalTax;
				for (Diner diner : dinerList)
				{
					diner.updateFinalTotal(subTotal, totalTax, roundTip);
				}
				round = true;
				editor.putBoolean("round", round);
				editor.commit();
			}

			grandTotalBox.setText("$"+String.format("%,.02f", finalTotalBill));
		}
		else if(v.getId()==R.id.addDinerButton)
			if(dinerList.size()<20)
			{
				//create table structure
		        TableLayout table = (TableLayout)findViewById(R.id.mainTable);
		        TableRow row = new TableRow(this);
		        TableRow row2 = new TableRow(this);
		        
		        //create diner components
		        EditText et1 = new EditText(this);
		        et1.setGravity(Gravity.RIGHT | Gravity.CENTER_VERTICAL);
		        EditText et2 = new EditText(this);
		        et2.setGravity(Gravity.CENTER);
		        TextView tv1 = new TextView(this);
		        tv1.setGravity(Gravity.RIGHT | Gravity.CENTER_VERTICAL);
		        TextView tv2 = new TextView(this);
		        tv2.setGravity(Gravity.CENTER);
		        ImageButton ib = new ImageButton(this);
		        
		        
		        //create diner
		        Diner diner = new Diner(et1, et2, ib, tv1, tv2, this);
		        dinerList.add(diner);
		        
		        //add stuff to category lists
		        buttonList.add(ib);
				amountList.add(et2);
				nameList.add(et1);
				
				//compose table
		        row.addView(et1);
		        row.addView(et2);
		        row.addView(ib);
		        //this part is to find the last row before the tip stuff
		        int rowIndex = 0;
		        for (int i = 0; i<dinerList.size()-1; i++)
		        {
		        	rowIndex += dinerList.get(i).editDollarList.size();
		        }
		        table.addView(row, rowIndex+1);
		        //update row index
		        rowIndex += 6+dinerList.size();
		        //+5 rows to get to bottom, +1 for the newly inserted row above, then + the diner list again to get to bottom
		        row2.addView(tv1);
		        row2.addView(tv2);
		        //extra +5 here is for the border line rows i added later
		        table.addView(row2, rowIndex+5);
		        
			}
			else
			{
				//Play negative sound effect
			}
		else if(buttonList.contains(v))
		{
			for (Diner dinerMax : dinerList)
			{
				if (dinerMax.button == v && dinerMax.editDollarList.size()<10)
				{
					//create table structure
					TableLayout table = (TableLayout)findViewById(R.id.mainTable);
					TableRow row = new TableRow(this);
					
					//create diner components
					EditText et = new EditText(this);
					et.setGravity(Gravity.CENTER);
					
					
					//edit diner by finding the right one first
					int rowIndex2 = 0;
					for (Diner buttonGuy : dinerList)
					{
						if (buttonGuy.button == v)
						{
							//calc another row index
							
							for (int i = 0; i<dinerList.indexOf(buttonGuy); i++)
							{
								rowIndex2 += dinerList.get(i).editDollarList.size();
							}
							rowIndex2 += buttonGuy.editDollarList.size();
							buttonGuy.newItem(et, this);
							

						}
					}
					
					//add stuff to category lists
					amountList.add(et);

					//construct table
					row.addView(et);
					table.addView(row, rowIndex2+1);

				}
				else
				{
					//negative sound effect
				}
			}
			
		}
		
	}

	public void onProgressChanged(SeekBar seekBar, int progress, boolean fromUser)
	{
		if (seekBar == tipBar && seek == true)
		{
			tipPercentValue = seekBar.getProgress();
			updateTip();
		}
	}

	private void updateTip()
	{
		seek = false;
		tipBar.setProgress(tipPercentValue);
		seek = true;
		tipPercentBox.setFilters(filter8);
		tipPercentBox.setText(Integer.toString(tipPercentValue)+"%");
		tipPercentBox.setFilters(filter3);
		totalTip = subTotal *  tipPercentValue * .01;
		if (round)
		{
			roundTip = Math.ceil(totalTip);
			tipDollarBox.setText("$"+String.format("%,.02f", roundTip));
			finalTotalBill = subTotal+roundTip+totalTax;
			for (Diner diner : dinerList)
			{
				diner.updateFinalTotal(subTotal, totalTax, roundTip);
			}
		}
		else
		{
			tipDollarBox.setText("$"+String.format("%,.02f", totalTip));
			finalTotalBill = subTotal+totalTip+totalTax;
			for (Diner diner : dinerList)
			{
				diner.updateFinalTotal(subTotal, totalTax, totalTip);
			}
			
		}
		
		
		grandTotalBox.setText("$"+String.format("%,.02f", finalTotalBill));
		editor.putInt("tip",tipPercentValue);
		editor.commit();
	}

	private void updateTax()
	{
		taxDollarBox.setFilters(filter16);
		taxDollarBox.setText("$"+String.format("%,.02f", totalTax));
		taxDollarBox.setFilters(filter8);
		if (round)
		{
			roundTip = Math.ceil(totalTip);
			finalTotalBill = subTotal+totalTax+roundTip;
			for (Diner diner : dinerList)
			{
				diner.updateFinalTotal(subTotal, totalTax, roundTip);
			}
		}
		else
		{
			finalTotalBill = subTotal+totalTax+totalTip;
			for (Diner diner : dinerList)
			{

				diner.updateFinalTotal(subTotal, totalTax, totalTip);
			}
		}
		grandTotalBox.setText("$"+String.format("%,.02f", finalTotalBill));

	}

	public void onStartTrackingTouch(SeekBar seekBar) 
	{
		// Not needed
		
	}

	public void onStopTrackingTouch(SeekBar seekBar) 
	{
		// Not needed
		
	}


	public void onFocusChange(View arg0, boolean arg1) {
		if(!arg0.hasFocus())
		{
			if (arg0 == tipPercentBox)
			{
				if (((EditText) arg0).getText().toString().contains("%") && ((EditText) arg0).getText().toString().length()<2)
				{
					((EditText) arg0).setText("0%");
				}
				else if (((EditText) arg0).getText().toString().length()<1)
				{
					((EditText) arg0).setText("0%");
				}
				tipPercentValue = Integer.parseInt(((EditText) arg0).getText().toString().replace("%",""));
				updateTip();
			}
			else if (arg0 == taxDollarBox)
			{
				if (((EditText) arg0).getText().toString().contains(".") && ((EditText) arg0).getText().toString().length()<2)
				{
					((EditText) arg0).setText("$0.00");
				}
				else if (((EditText) arg0).getText().toString().contains("$") && ((EditText) arg0).getText().toString().length()<2)
				{
					((EditText) arg0).setText("$0.00");
				}
				else if (((EditText) arg0).getText().toString().length()<1)
				{
					((EditText) arg0).setText("$0.00");
				}
				totalTax = Double.parseDouble(((EditText) arg0).getText().toString().replace("$","").replace(",",""));
				updateTax();
			}
			else if(amountList.contains(arg0))
			{
				if (((EditText) arg0).getText().toString().contains(".") && ((EditText) arg0).getText().toString().length()<2)
				{
					((EditText) arg0).setText("$0.00");
				}
				else if (((EditText) arg0).getText().toString().contains("$") && ((EditText) arg0).getText().toString().length()<2)
				{
					((EditText) arg0).setText("$0.00");
				}
				else if (((EditText) arg0).getText().toString().length()<1)
				{
					((EditText) arg0).setText("$0.00");
				}
				for (Diner diner1 : dinerList)
				{
					if (diner1.editDollarList.contains(arg0))
					{
						subTotal -= diner1.preTaxTotal;
						diner1.updateSubTotal();
						subTotal += diner1.preTaxTotal;
					}
				}
				updateTip();
				
				
			}
			else if (nameList.contains(arg0))
			{
				System.out.println("test");
				for (Diner nameDiner : dinerList)
				{
					if (nameDiner.editName == arg0)
					{
						nameDiner.setName();
					}
				}
			}
		}

		
	}
	private void getBg()
	{
		if (bgIndex == 0)
		{
    		bg.setBackgroundDrawable(null);
		}
		else if (bgIndex == 1)
		{
			bg.setBackgroundResource(R.drawable.one);
		}
		else if (bgIndex == 2)
		{
			bg.setBackgroundResource(R.drawable.two);
		}
		else if (bgIndex == 3)
		{
			bg.setBackgroundResource(R.drawable.three);
		}
		else if (bgIndex == 4)
		{
			bg.setBackgroundResource(R.drawable.four);
		}
		else if (bgIndex == 5)
		{
			bg.setBackgroundResource(R.drawable.five);
		}
		else if (bgIndex == 6)
		{
			bg.setBackgroundResource(R.drawable.six);
		}
		else if (bgIndex == 7)
		{
			bg.setBackgroundResource(R.drawable.seven);
		}
		else if (bgIndex == 8)
		{
			bg.setBackgroundResource(R.drawable.eight);
		}
		else if (bgIndex == 9)
		{
			bg.setBackgroundResource(R.drawable.nine);
		}
		else if (bgIndex == 10)
		{
			bg.setBackgroundResource(R.drawable.ten);
		}
		else if (bgIndex == 11)
		{
			bg.setBackgroundResource(R.drawable.eleven);
		}
		else if (bgIndex == 12)
		{
			bg.setBackgroundResource(R.drawable.twelve);
		}
		else if (bgIndex == 13)
		{
			bg.setBackgroundResource(R.drawable.thirteen);
		}
		else if (bgIndex == 14)
		{
			bg.setBackgroundResource(R.drawable.fourteen);
		}
		else if (bgIndex == 15)
		{
			bg.setBackgroundResource(R.drawable.fifteen);
		}

	}
}


