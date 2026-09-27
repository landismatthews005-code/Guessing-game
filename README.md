# Guessing-game 

math.randomseed(os.time())

local playing = true

while playing do

    local targetNumber = math.random(1,100) 
    local maxAttempts = 7
    local attemptsUsed = 0
    local hasWon = false

print ("Welcome to my guessing game.")
print ("I am thinking of a number between 1 and 100.")
print("You have" ..maxAttempts.. "to guess the right number.")

while attemptsUsed < maxAttempts and not hasWon do
    attemptsUsed = attemptsUsed + 1
    local remainingAttempts = maxAttempts - attemptsUsed
    
    io.write("\nAttempt " .. attemptsUsed .. "/" .. maxAttempts .. " - Enter your guess: ")
    local input = io.read()

    -- Error Handling: Convert input to a number and validate it
    local guess = tonumber(input)

    if not guess then
        print("Invalid input! Please enter a number, not letters or symbols.")
        -- Give the attempt back since it was an invalid input
        attemptsUsed = attemptsUsed - 1 
    elseif guess < 1 or guess > 100 then
        print("Out of range! Please guess a number between 1 and 100.")
        -- Give the attempt back since it was out of bounds
        attemptsUsed = attemptsUsed - 1
    else
        -- Check the guess and see if it is correct and give feed back for better guess.
        if guess == targetNumber then
            hasWon = true
        elseif guess < targetNumber then
            print("Too low! Try a higher number.")
            if remainingAttempts > 0 then
                print("You have " .. remainingAttempts .. " attempts left.")
            end
        else
            print("Too high! Try a lower number.")
            if remainingAttempts > 0 then
                print("You have " .. remainingAttempts .. " attempts left.")
            end
        end
    end
end
 -- End of game messages
   
    if hasWon then
        print(" Congratulations! You won!")
        print("You guessed the number (" .. targetNumber .. ") in " .. attemptsUsed .. " attempts.")
        print("press enter")
    else
        print("Game Over! You are out of attempts.")
        print("The correct number was: " .. targetNumber)
        print("press enter to continue")
    end


    -- Ask the player if they want to play again
    local validChoice = false
    while not validChoice do
        io.write("\nDo you want to play again? (y/n): ")
        local choice = io.read() 

        if choice == "y" or choice == "yes" then
            validChoice = true
        elseif choice == "n" or choice == "no" then
            validChoice = true
            playing = false
            print("\nThank you for playing! Goodbye!")
        else
            print("Please type 'y' for yes or 'n' for no.")
        end
    end
end
