# repos
// pre-processor directives
#include "pch.h"
#include <iostream>
#include <string>
#include <string.h>
#include <fstream>
#include <time.h>

using namespace std;

int main(void)
{
	
	//variables
	string name = " ";
	string name2 = " ";
	string title = " ";
	string title2 = " ";
	string faction = " ";
	string faction2 = " ";
	string specialItem = " ";
	string specialItem2 = " ";
	int health = 0;
	int health2 = 0;
	int strength = 0;
	int strength2 = 0;
	int defense = 0;
	int defense2 = 0;
	int luck = 0;
	int luck2 = 0;
	int leftover = 0;
	int charChoice = 0;

	string StatsPath = "Characters\\";
	string RosterPath = "Characters\\Roster.txt";
	string logPath = "Characters\\duelLog.txt";
	

	int userChoice = 0;

	fstream Stats;
	fstream Roster;
	fstream duelLog;

	while (true)
	{

		int userInput = 0;

		system("cls");
		cout << "Menu" << endl;
		cout << "------------------" << endl;
		cout << "1. Create a Character" << endl;
		cout << "2. Delete a Character" << endl;
		cout << "3. Duel" << endl;
		cout << "4. Quit Game" << endl;
		cout << "What would you like to do?" << endl;
		cin >> userInput;
		if (userInput == 1)
		{
			system("cls");

			while (true)
			{
				//menu2
				cout << "How do you want to create your character" << endl;
				cout << "------------------------------------------" << endl;
				cout << "1. Manually" << endl;
				cout << "2. Randomly" << endl;
				cout << "------------------------------------------" << endl;
				cout << "Choice: ";
				cin >> charChoice;
				cin.ignore();
				system("cls");

				if (charChoice == 1)//create a character manually
				{
					cout << "Creating Player" << endl;
					cout << "------------------------------------------" << endl;
					cout << "Enter a name:\n";
					getline(cin, name);

					cout << "\nEnter a title:\n";
					getline(cin, title);

					cout << "\nEnter amount of health:\n";
					cin >> health;

					cout << "\nEnter amount of strength:\n";
					cin >> strength;

					//check that value does not exceed 180. 
					if (strength > 179)
					{
						strength = 1;
					}

					leftover = 180 - strength;

					cout << "Enter amount of defense:\n\n";
					cin >> defense;

					//check that value does not exceed amount of leftover attribute points
					if (defense > leftover)
					{
						defense = 1;
					}

					leftover = leftover - defense;

					cout << "Enter amount of luck:\n\n";
					cin >> luck;

					//check that value does not exceed amount of leftover attribute points
					if (luck > leftover)
					{
						luck = 1;
					}

					//Determining Player 1 faction and special item
					//Strength is greatest
					if ((strength > defense) && (strength > luck))
					{
						faction = "Wolves";
						specialItem = "Sword";
					}

					//Defense is greatest
					else if ((defense > strength) && (defense > luck))
					{
						faction = "Ape";
						specialItem = "Armor";
					}

					//Luck is greatest
					else if ((luck > strength) && (luck > defense))
					{
						faction = "Cat";
						specialItem = "Coincidence";
					}

					//default
					else
					{
						faction = "Cat";
						specialItem = "Coincidence";
					}

					//print to screen
					cout << "Character Created" << endl;
					cout << "------------------" << endl;
					cout << name << endl;
					cout << title << endl;
					cout << health << endl;
					cout << strength << endl;
					cout << defense << endl;
					cout << luck << endl;
					cout << faction << endl;
					cout << specialItem << endl;
					cout << "------------------" << endl;
					system("pause");
					system("cls");

					//create text file using name of student
					Stats.open(StatsPath + name + ".txt", ios::out);

					//store stats to file
					Stats << name << endl;
					Stats << title << endl;
					Stats << health << endl;
					Stats << strength << endl;
					Stats << defense << endl;
					Stats << luck << endl;

					//close file
					Stats.close();

					//open roster file
					Roster.open(RosterPath, ios::app);

					//add the name to the file
					Roster << name << endl;

					//close file
					Roster.close();

				}
				else if (charChoice == 2)
				{
					int soRandom = 0;
					//Seed random number generator
					srand((unsigned)time(NULL));
					//Generate random number between 1 and 10
					{soRandom = (rand() % 10) + 1;

					//Option 1
					if (soRandom <= 3)
					{
						name2 = " Richard Parker";
						title2 = " Luckiest Cat ever";
						health2 = 100;
					}

					//Option 2
					else if ((soRandom > 3) && (soRandom <= 7))
					{
						name2 = " Brian May";
						title2 = " Guitar God";
						health2 = 100;
					}

					//Option 3
					else if (soRandom > 7)
					{
						name2 = "Bruce Banner";
						title2 = "The Incredible Hulk";
						health2 = 100;
					}
					}
					strength2 = (rand() % 180) + 1;
					defense2 = (rand() % (180 - strength2)) + 1;
					luck2 = 180 - strength2 - defense2;

					//print to screen
					cout << "Character Created" << endl;
					cout << "------------------" << endl;
					cout << name2 << endl;
					cout << title2 << endl;
					cout << health2 << endl;
					cout << strength2 << endl;
					cout << defense2 << endl;
					cout << luck2 << endl;
					cout << "------------------" << endl;
					system("pause");

					//Determining Player 2 faction and special item
					//Strength is greatest
					if ((strength2 > defense2) && (strength2 > luck2))
					{
						faction2 = "Wolves";
						specialItem2 = "Sword";
					}

					//Defense is greatest
					else if ((defense2 > strength2) && (defense2 > luck2))
					{
						faction2 = "Ape";
						specialItem2 = "Armor";
					}

					//Luck is greatest
					else if ((luck2 > strength2) && (luck2 > defense2))
					{
						faction2 = "Cat";
						specialItem2 = "Coincidence";
					}
					else
						//default
					{
						faction = "Cat";
						specialItem = "Coincidence";
					}
				}

				break;
			}
		}
		else if (userInput == 3)
		{
			int dueloption = 0;
			bool isActive = true;
			while (isActive)
			{
				string tempName = " ";
				string tempTitle = " ";
				int tempHealth = 100;
				int tempStrength = 0;
				int tempDefense = 0;
				int tempLuck = 0;
				string tempName2 = " ";
				string tempTitle2 = " ";
				int tempHealth2 = 100;
				int tempStrength2 = 0;
				int tempDefense2 = 0;
				int tempLuck2 = 0;

				cout << "Duel Options" << endl;
				cout << "-------------------------------" << endl;
				cout << "1. Player 1 vs Player 2" << endl;
				cout << "2. Player 1 vs Computer" << endl;
				cout << "3. Return to Main Menu" << endl;
				cout << "-------------------------------" << endl;
				cout << "Choice: " << endl;

				cin >> dueloption;
				if (dueloption == 1)
				{
					int createChar1;
					cout << "Player 1 Character Selection" << endl;
					cout << "--------------------------------------------------" << endl;
					cout << "1. Load Character" << endl;
					cout << "2. Random Character" << endl;
					cout << "--------------------------------------------------" << endl;
					cout << "Choice: " << endl;

					cin >> createChar1;

					if (createChar1 == 1)
					{
						string studentSel;
				
						// opening roster
						Roster.open(RosterPath, ios::in);

						cout << "Student in Roster" << endl;
						cout << "-----------------------------------" << endl;

						//creating while loop to move through all contents in the file
						while (!Roster.eof())
						{
							string temp;
							getline(Roster, temp);
							cout << temp << endl;
						} // end while
						cout << "------------------------------------" << endl;

						// close the roster
						Roster.close();

						// ask the user to pick a name from the list
						cout << endl;
						cout << "Which student would you like to load?" << endl;
						cin >> studentSel;

						// opening the file
						Stats.open(StatsPath + studentSel + ".txt", ios::in);

						// check to see if the student exists
						if (Stats.good()) // good is a function part of fstream, gives true or fals value (in this case does name exist?
						{
							

							// reading from the file (loading values), need to list the order that we recieve the information (order is important)
							Stats >> tempName;
							Stats >> tempTitle;
							Stats >> tempHealth;
							Stats >> tempStrength;
							Stats >> tempDefense;
							Stats >> tempLuck;

							if ((tempStrength > tempDefense) && (tempStrength > tempLuck))
							{
								faction = "Wolves";
								specialItem = "Sword";
							}

							//Defense is greatest
							else if ((tempDefense > tempStrength) && (tempDefense > tempLuck))
							{
								faction = "Ape";
								specialItem = "Armor";
							}

							//Luck is greatest
							else if ((tempLuck > tempStrength) && (tempLuck > tempDefense))
							{
								faction = "Cat";
								specialItem = "Coincidence";
							}
							else
								//default
							{
								faction = "Cat";
								specialItem = "Coincidence";
							}

							// print stats to screen
							cout << tempName << "Stats" << endl;
							cout << "-------------------------------------------------------" << endl;
							cout << tempName << endl;
							cout << tempTitle << endl;
							cout << tempHealth << endl;
							cout << tempStrength << endl;
							cout << tempDefense << endl;
							cout << tempLuck << endl;
							cout << faction << endl;
							cout << specialItem << endl;
							cout << "-------------------------------------------------------" << endl;
							system("pause");
							system("cls");

						} // end if (true, student exists)

						else
						{
							cout << "Student does not exist... try again later" << endl;
						} // end else, false if student name doesn't exist

						Stats.close();
					} // end else if (userChoice == 2)

					else if (userChoice == 3)
					{
						cout << "goodbye" << endl;
						system("pause");
						isActive = false; // stop the loop, could do a break statement as well
					} // end else if (userChoice == 3)
					else if (createChar1 == 2)
					{
						int health1 = 100;
						int soRandom = 0;
						//Seed random number generator
						srand((unsigned)time(NULL));
						//Generate random number between 1 and 10
						{soRandom = (rand() % 10) + 1;

						//Option 1
						if (soRandom <= 3)
						{
							name2 = " Richard Parker";
							title2 = " Luckiest Cat ever";
							
						}

						//Option 2
						else if ((soRandom > 3) && (soRandom <= 7))
						{
							name2 = " Brian May";
							title2 = " Guitar God";
							
						}

						//Option 3
						else if (soRandom > 7)
						{
							name2 = "Bruce Banner";
							title2 = "The Incredible Hulk";
				
						}
						}
						strength2 = (rand() % 180) + 1;
						defense2 = (rand() % (180 - strength2)) + 1;
						luck2 = 180 - strength2 - defense2;

						//print to screen
						cout << "Character Created" << endl;
						cout << "------------------" << endl;
						cout << name2 << endl;
						cout << title2 << endl;
						cout << health2 << endl;
						cout << strength2 << endl;
						cout << defense2 << endl;
						cout << luck2 << endl;
						cout << "------------------" << endl;
						system("pause");

						//Determining Player 2 faction and special item
						//Strength is greatest
						if ((strength2 > defense2) && (strength2 > luck2))
						{
							faction2 = "Wolves";
							specialItem2 = "Sword";
						}

						//Defense is greatest
						else if ((defense2 > strength2) && (defense2 > luck2))
						{
							faction2 = "Ape";
							specialItem2 = "Armor";
						}

						//Luck is greatest
						else if ((luck2 > strength2) && (luck2 > defense2))
						{
							faction2 = "Cat";
							specialItem2 = "Coincidence";
						}
						else
							//default
						{
							faction = "Cat";
							specialItem = "Coincidence";
						}
					}
					int createChar2 = 0;
					cout << "Player 2 Character Selection" << endl;
					cout << "--------------------------------------------------" << endl;
					cout << "1. Load Character" << endl;
					cout << "2. Random Character" << endl;
					cout << "--------------------------------------------------" << endl;
					cout << "Choice: " << endl;

					cin >> createChar2;

					if (createChar2 == 1)
					{
						string studentSel;

						// opening roster
						Roster.open(RosterPath, ios::in);

						cout << "Student in Roster" << endl;
						cout << "-----------------------------------" << endl;

						//creating while loop to move through all contents in the file
						while (!Roster.eof())
						{
							string temp;
							getline(Roster, temp);
							cout << temp << endl;
						} // end while
						cout << "------------------------------------" << endl;

						// close the roster
						Roster.close();

						// ask the user to pick a name from the list
						cout << endl;
						cout << "Which student would you like to load?" << endl;
						cin >> studentSel;

						// opening the file
						Stats.open(StatsPath + studentSel + ".txt", ios::in);

						// check to see if the student exists
						if (Stats.good()) // good is a function part of fstream, gives true or fals value (in this case does name exist?
						{
							

							// reading from the file (loading values), need to list the order that we recieve the information (order is important)
							Stats >> tempName2;
							Stats >> tempTitle2;
							Stats >> tempHealth2;
							Stats >> tempStrength2;
							Stats >> tempDefense2;
							Stats >> tempLuck2;

							if ((tempStrength2 > tempDefense2) && (tempStrength2 > tempLuck2))
							{
								faction2 = "Wolves";
								specialItem2 = "Sword";
							}

							//Defense is greatest
							else if ((tempDefense2 > tempStrength2) && (tempDefense2 > tempLuck2))
							{
								faction2 = "Ape";
								specialItem2 = "Armor";
							}

							//Luck is greatest
							else if ((tempLuck2 > tempStrength2) && (tempLuck2 > tempDefense2))
							{
								faction2 = "Cat";
								specialItem2 = "Coincidence";
							}
							else
								//default
							{
								faction2 = "Cat";
								specialItem2 = "Coincidence";
							}

							// print stats to screen
							cout << tempName2 << "Stats" << endl;
							cout << "-------------------------------------------------------" << endl;
							cout << tempName2 << endl;
							cout << tempTitle2 << endl;
							cout << tempHealth2 << endl;
							cout << tempStrength2 << endl;
							cout << tempDefense2 << endl;
							cout << tempLuck2 << endl;
							cout << faction2 << endl;
							cout << specialItem2 << endl;
							cout << "-------------------------------------------------------" << endl;
							system("pause");
							system("cls");

						} // end if (true, student exists)

						else
						{
							cout << "Student does not exist... try again later" << endl;
						} // end else, false if student name doesn't exist

						Stats.close();
					} // end else if (userChoice == 2)

					else if (userChoice == 3)
					{
						cout << "goodbye" << endl;
						system("pause");
						isActive = false; // stop the loop, could do a break statement as well
					} // end else if (userChoice == 3)
					if (createChar2 == 2)
					{
						health2 = 100;
						int soRandom = 0;
						//Seed random number generator
						srand((unsigned)time(NULL));
						//Generate random number between 1 and 10
						{soRandom = (rand() % 10) + 1;

						//Option 1
						if (soRandom <= 3)
						{
							name2 = " Richard Parker";
							title2 = " Luckiest Cat ever";
							health2 = 100;
						}

						//Option 2
						else if ((soRandom > 3) && (soRandom <= 7))
						{
							name2 = " Brian May";
							title2 = " Guitar God";
							health2 = 100;
						}

						//Option 3
						else if (soRandom > 7)
						{
							name2 = "Bruce Banner";
							title2 = "The Incredible Hulk";
							health2 = 100;
						}
						}
						strength2 = (rand() % 180) + 1;
						defense2 = (rand() % (180 - strength2)) + 1;
						luck2 = 180 - strength2 - defense2;

						//print to screen
						cout << "Character Created" << endl;
						cout << "------------------" << endl;
						cout << name2 << endl;
						cout << title2 << endl;
						cout << health2 << endl;
						cout << strength2 << endl;
						cout << defense2 << endl;
						cout << luck2 << endl;
						cout << "------------------" << endl;
						system("pause");

						//Determining Player 2 faction and special item
						//Strength is greatest
						if ((strength2 > defense2) && (strength2 > luck2))
						{
							faction2 = "Wolves";
							specialItem2 = "Sword";
						}

						//Defense is greatest
						else if ((defense2 > strength2) && (defense2 > luck2))
						{
							faction2 = "Ape";
							specialItem2 = "Armor";
						}

						//Luck is greatest
						else if ((luck2 > strength2) && (luck2 > defense2))
						{
							faction2 = "Cat";
							specialItem2 = "Coincidence";
						}
						else
							//default
						{
							faction = "Cat";
							specialItem = "Coincidence";
						}
					}
					else if (dueloption == 2)
					{
						cout << "That function is not available yet." << endl;
					}

					//start duel
					//int health1 = 100;
					//health2 = 100;
					if ((tempHealth != 0) && (tempHealth2 != 0))

					{
						system("cls");

						//Print player 1 stats
						cout << "Player 1 Stats" << endl;
						cout << "----------------------------------" << endl;
						cout << "Name: " << tempName << endl;
						cout << "Title: " << tempTitle << endl;
						cout << "Health: " << tempHealth << endl;
						cout << "Strength: " << tempStrength << endl;
						cout << "Defense: " << tempDefense << endl;
						cout << "Luck: " << tempLuck << endl;
						cout << "Faction: " << faction << endl;
						cout << "Sp.Item: " << specialItem << endl;
						cout << "----------------------------------\n\n" << endl;

						//Print player 2 stats
						cout << "Player 2 Stats" << endl;
						cout << "----------------------------------" << endl;
						cout << "Name: " << tempName2 << endl;
						cout << "Title: " << tempTitle2 << endl;
						cout << "Health: " << tempHealth2 << endl;
						cout << "Strength: " << tempStrength2 << endl;
						cout << "Defense: " << tempDefense2 << endl;
						cout << "Luck: " << tempLuck2 << endl;
						cout << "Faction: " << faction2 << endl;
						cout << "Sp.Item: " << specialItem2 << endl;
						cout << "----------------------------------\n\n" << endl;
						//Print rules
						cout << "Rules\n" << endl;
						cout << "--------------------------------------------------" << endl;
						cout << "Player 1 will duel Player 2 in a fight to the death." << endl;
						cout << "Both players will alternate turns." << endl;
						cout << "Players will have three choices each turn/n" << endl;
						cout << "1. Attack" << endl;
						cout << "2. Use an Item" << endl;
						cout << "3. Forfiet" << endl;
						cout << "--------------------------------------------------\n\n" << endl;
						system("pause");
						system("cls");
						cout << "Press enter when you are ready" << endl;

						int roundcount = 0;
						health = 100;
						health2 = 100;
						//while either player is alive, display Player1 turn
						while ((health > 0) || (health2 > 0))
						{

							int duelchoice = 0;
							int damage = 0;

							roundcount = roundcount + 1;
							cout << "\n Round: " << roundcount << "  Player 1 Turn" << endl;
							cout << "------------------------------------------" << endl;
							cout << "1. Attack" << endl;
							cout << "2. Item" << endl;
							cout << "3. Forfiet" << endl;
							cout << "------------------------------------------" << endl;
							cout << "Choice : " << endl;
							cin >> duelchoice;
							//Player 1 attacks, print damage 
							if (duelchoice == 1)
							{
								damage = (rand() % 20) + 1;
								health2 = health2 - damage;
								cout << "Player 1 wielded " << damage << " damage." << endl;
								// if the other player dies as a result of the atatck
								if (health2 <= 0)
								{
									cout << "Player 2 has died.";
								}
								// if the other player does not die, print updated health
								else
								{
									cout << "Player 2 has " << health2 << " health." << endl;
								}
								system("pause");
								system("cls");
							}
							//use item
							else if (duelchoice == 2)
							{
								
								cout << "This feature is not yet available." << endl;
							}
							//user forfeits game
							else if (duelchoice == 3)
							{
								cout << "Player 1 has forfeited the game." << endl;
								exit(1);
							}
							//if other player is dead after player 1 turn, print game results and record in Duel Log
							if ((health <= 0) || (health2 <= 0))
							{
								duelLog.open(logPath, ios::app);
								duelLog << "\n\nGame Results" << endl;
								duelLog << "------------------------------------------" << endl;
								cout << "\n\nGame Results" << endl;
								cout << "------------------------------------------" << endl;
								duelLog << "Number of Rounds : " << roundcount << endl;
								cout << "Number of Rounds : " << roundcount << endl;
								//Player 2 wins
								if (health <= 0)
								{
									cout << "Winner : Player 2" << endl;
									cout << "------------------------------------------" << endl;
									cout << "Game over" << endl;
									duelLog << "Winner : Player 2" << endl;
									duelLog << "------------------------------------------" << endl;
									duelLog << "Game over" << endl;
									break;
								}
								//Player 1 wins
								else
								{
									duelLog << "Winner : Player 1" << endl;
									duelLog << "------------------------------------------" << endl;
									duelLog << "Game over" << endl;
									cout << "Winner : Player 1" << endl;
									cout << "------------------------------------------" << endl;
									cout << "Game over" << endl;
									break;
								}
								duelLog.close();
							}
							//Player 2 Menu
							cout << "\n Round: " << roundcount << "  Player 2 Turn" << endl;
							cout << "------------------------------------------" << endl;
							cout << "1. Attack" << endl;
							cout << "2. Item" << endl;
							cout << "3. Forfiet" << endl;
							cout << "------------------------------------------" << endl;
							cout << "Choice : " << endl;
							cin >> duelchoice;
							//Player 2 chooses attack, print damage
							if (duelchoice == 1)
							{
								damage = (rand() % 20) + 1;
								health = health - damage;
								cout << "Player 2 wielded " << damage << " damage." << endl;
								//If player 1 dies after player 2 turn
								if (health <= 0)
								{
									cout << "Player 1 has died." << endl;
								}
								else
									//If player 1 does not die, update health
								{
									cout << "Player 1 has " << health << " health." << endl;
									system("pause");
									system("cls");
								}

							}
							// use item
							else if (duelchoice == 2)
							{
								cout << "This feature is not yet available." << endl;
							}
							//user forfeits game
							else if (duelchoice == 3)
							{
								cout << "Player 2 has forfeited the game." << endl;
								exit(1);
							}

							//if either player dies, print game results, and record in Duel Log
							if ((health <= 0) || (health2 <= 0))
							{
								duelLog.open(logPath, ios::app);

								cout << "Game Results" << endl;
								cout << "------------------------------------------" << endl;
								cout << "Number of Rounds : " << roundcount << endl;
								duelLog << "Game Results" << endl;
								duelLog << "------------------------------------------" << endl;
								duelLog << "Number of Rounds : " << roundcount << endl;
								if (health <= 0)
								{
									//player 2 wins
									cout << "Winner : Player 2" << endl;
									cout << "------------------------------------------" << endl;
									cout << "Game over" << endl;
									duelLog << "Winner : Player 2" << endl;
									duelLog << "------------------------------------------" << endl;
									duelLog << "Game over" << endl;
								}
								else
								{
									//player 1 wins
									cout << "Winner : Player 1" << endl;
									cout << "------------------------------------------" << endl;
									cout << "Game over" << endl;
									duelLog << "Winner : Player 1" << endl;
									duelLog << "------------------------------------------" << endl;
									duelLog << "Game over" << endl;
								}
								duelLog.close();
								break;
							}
							//clear screen
							system("cls");
						}
					}
					
				}
				else if (userInput == 4)
				{//exit the program
					exit(1);
				}
				else if (dueloption == 2)
				{
					cout << "This function is not available yet." << endl;
				}
				else
				{
					//user picks an option other than 1, 2, 3, or 4
					cout << "Invalid Option" << endl;
					continue;
				}

				system("pause");
				system("cls");
			}
		}
}}
