#FORMATTING VARIABLES
 	@bar = '|'
 	@bookend = '+ -=- +'
	@header_line   ='+-=-=-=-=-=-=-=-=-=-=-=-=-=-==-=-=-=-=-=-=-=-=-=-=-=-=-=-=-+'		#@header_line need be divisible by 2 & 4 to properly
	@standard_line ='<><><><><><><>--------------------------------<><><><><><><>'		  #center given my formatting methods [chose 60 chars]
	@lineWidth = @header_line.length 
	@welcome = 'WELCOME TO RUBY TIC-TAC-TOE'
	@instruct = 'INSTRUCTIONS'
	@instruct_L1 = 'Make moves by typing a column letter and row #.'
	@instruct_L2 = 'Example: "A1" -> marks the top-left square.'
 	@name_input = 'Hello! What\'s your name?'
	
#FORMATTING METHODS
	def header
		puts
		puts @header_line
		puts @bar.ljust(@lineWidth/4) + @welcome.center(@lineWidth/2) + @bar.rjust((@lineWidth/4))
		puts @header_line
		puts
	end
	def put_line
		puts
		puts @standard_line
		puts
	end
	def borders 
		puts @bar.ljust(@lineWidth/2) + @bar.rjust(@lineWidth/2)
	end
	def instructions
		puts @header_line
		puts @bar.ljust(@lineWidth/4) + @instruct.center(@lineWidth/2) + @bar.rjust((@lineWidth/4))
		puts @header_line
		puts @instruct_L1.center@lineWidth
		puts @instruct_L2.center@lineWidth
		puts @header_line
		puts
	end
	def centered (text)
		puts text.center(@lineWidth)
	end
	def board_setup									
		puts 
		puts "#{@robbie_name}: #{@robbie}"
		puts "#{@user_name}: #{@user}"
		puts 
		puts '    A B C'
		puts 
		puts " 1  #{@squares["A1"]}|#{@squares["B1"]}|#{@squares["C1"]}"
		puts "    -+-+-"
		puts " 2  #{@squares["A2"]}|#{@squares["B2"]}|#{@squares["C2"]}"
		puts "    -+-+-"
		puts " 3  #{@squares["A3"]}|#{@squares["B3"]}|#{@squares["C3"]}"
	end

#FUNCTIONAL VARIABLES
	@robbie = rand() > 0.5 ? 'X' : 'O'
	@user = @robbie == 'X' ? 'O' : 'X'
	@robbie_name = 'Robbie the Robot'									#For what it's worth, the robot's name is based off my 1990's childhood 
	@columns = 	['A','B','C']											  #yellow robot piggybank. The play-on-words only felt appropriate.
	@rows =		['1','2','3']
	STDOUT.sync = true
	@squares = {
		"A1"=>" ","A2"=>" ","A3"=>" ",									#Sets up the squares as hashes with ' ' values to start.
		"B1"=>" ","B2"=>" ","B3"=>" ",
		"C1"=>" ","C2"=>" ","C3"=>" "
		}
	@solution_set = [													#Defines the array of all winning array combinations.
		['A1','A2','A3'],
		['B1','B2','B3'],
		['C1','C2','C3'],
		['A1','B1','C1'],
		['A2','B2','C2'],
		['A3','B3','C3'],
		['A1','B2','C3'],
		['C1','B2','A3']
		]

#FUNCTIONAL METHODS
	def user_turn
		board_setup
		puts
		puts 'Type a letter and number [ie "A1"] to mark a square.'
		puts ' +--> Type "Restart" at any point to start over.'
		input = gets.chomp.upcase
		put_line
		if input.length == 2
			selection = input.split('')
			if((@columns.include? selection[0]) && (@rows.include? selection[1]) && @squares[input] == ' ')
				@squares[input] = @user
				centered "#{@user_name} drew an #{@user} in #{input}."
				winner_winner?(@robbie)
			else 
				invalid
			end
		else 
			invalid unless input == "RESTART"
		end
	end
	def robbie_turn
		move = game_logic
		@squares[move] = @robbie
		centered "#{@robbie_name} drew an #{@robbie} in #{move}."
		winner_winner?(@user)
	end
	def game_logic
		@solution_set.each do |solution|								#Evaluates each array for 2 @robbie marks and an open square.
			if mark_count_in_square_arrays(solution, @robbie) == 2	
				return empty_count_in_square_arrays solution 			#If true, @robbie runs method to square game-winning mark.
			end															#An explicit return statement is required to exit the current subroutine,
			end															  #and use the returened value in the code immediately following it.
		@solution_set.each do |solution|								
			if mark_count_in_square_arrays(solution, @user) == 2		#Evaluates each array for 2 @user marks and an open sqaure.
				return empty_count_in_square_arrays solution 			#If true, @robbie runs method to prevent user victory.
			end
			end
		@solution_set.each do |solution|
			if mark_count_in_square_arrays(solution, @robbie) == 1
				return empty_count_in_square_arrays solution
			end
			end															
		s = @squares.keys;
		i = rand(s.length)												#Random square selection made from those '' squares.
			if @squares[s[i]] == " "									
				return s[i]												#Explicitly returns a random square of syntax 'A1' for the "move" variable
			else  														  #in the robbie_turn method
			@squares.each do |space,value| return space if value == " "	#Selections made from open squares in ascending order staring with key 1.
			end
			end
		end
	def mark_count_in_square_arrays square, mark
		mark_count = 0
		square.each do |i|
			mark_count += 1 if @squares[i] == mark						#Code loop evaluates each square array to count the # of robbie's marks [@robbie]
	  		unless @squares[i] == mark || @squares[i] == ' '			#If the user has a mark (not blank or robbie mark) within the squares array 
				return 0												#being evalutated, code sets the marks variable to '0' to inform the
			end															#game logic not to put another robbie mark in that array.
		end
		mark_count
	end
	def empty_count_in_square_arrays square
		square.each do |i|
			if @squares[i] == " "
				return i
			end
		end
	end
	def invalid
		put_line
		puts 'Please use format "A1", "B2", etc; and select an empty box.'
		user_turn
	end
	def winner_winner?next_turn
		game_over = ()													#Evaluates if robbie has won
		@solution_set.each do |solution|
			if mark_count_in_square_arrays(solution, @robbie) == 3
				board_setupz
				put_line
				puts 'You lost... Please try harder next time. :)'
				puts
				game_over = true
			end
			if mark_count_in_square_arrays(solution, @user) == 3		#Evaluates if user has won
				board_setup
				put_line
				puts 'You actually won... Can\'t say I\'m not surprised...'
				puts
				game_over = true
			end
		end
		unless game_over												
			if(move_countdown > 0) && (next_turn == @user)				#If not game_over, and there are still spaces left, next few lines of code 
				user_turn												  #evaluate if it's the user's turn, or robbie's. If neither, than it's a cats game.
			else
				if next_turn == @robbie
					robbie_turn
				else
					board_setup
					@put_line
					puts 'Cat\'s game!  Rubber match?'
					puts
				end
			end
		end
	end
	def move_countdown
		blanks = 0
			@squares.each do |square, mark|
			if mark == " "
				blanks = (blanks + 1)									#Loops adding 1 for each empty square using implicit returns.
			end
			end
		blanks
	end
	
#EXECUTES GAME SETUP
	puts @name_input
	@user_name = gets.chomp.capitalize
	header
	centered (@user_name + ', let this be said:')
	centered 'The gauntlet has been thrown down,'						#Goodwill Hunting reference
	centered 'But Robbie will answer, and will answer with vigor!'
	put_line
	centered "MAY THE ODDS BE EVER IN YOUR FAVOR!"
	put_line
	instructions

#EXECUTES GAMEPLAY
	if(@user == 'X')
		puts
		puts 'Lucky you! You drew X\'s and therefore get to start.'
		puts 'It\'s your move!'
		user_turn
	else
		centered "#{@robbie_name} drew X\'s'. X\'s have the first move."
		robbie_turn
	end

