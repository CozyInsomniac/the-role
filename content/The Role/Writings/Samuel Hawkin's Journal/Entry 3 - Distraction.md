December 27, 2020 | 2:00 PM EST

I wrote a Python program today. It creates a musical harmonic scale based on user-input.
Here it is:

```
"""
File:	minor_key.py
Author:  Samuel Hawkins
Date:	December 27, 2021
Description: Creates an harmonic scale based on a user-inputted regular or flat note.
"""

#Defining global constants
MUSICAL_NOTES = ['C', 'D\u266d', 'D', 'E\u266d', 'E', 'F', 'G\u266d', 'G', 'A\u266d', 'A', 'B\u266d', 'B']
BLANK_SEPARATOR = ""


#Defining convert_note function
def convert_note(raw_note):
	"""
The convert_note function will accept a user-inputted note and convert it into a program-readable format.
	(Ex: "G flat" will become "G\u266d")

	:param raw_note: the user-inputted note string that will be converted
	:return: the program-readable format of the note
	"""

	# Converting "flat" notes
	if "flat" in raw_note:
		split_note = raw_note.upper().split()
		split_note.remove("FLAT")
		split_note.append("\u266d")
		converted_note = BLANK_SEPARATOR.join(split_note)
		return converted_note

	#Converting regular notes
	elif raw_note.upper() in MUSICAL_NOTES:
		converted_note = raw_note.upper()
		return converted_note

	# Invalid input handler
	else:
		converted_note = raw_note.upper()
		return converted_note


#Defining octave_create function
def octave_create(converted_note):
	"""
The octave_create function will create a harmonic scale based on the user-given note.

:param converted_note: The musical-notation converted note that was based on user input
	"""
	# Setting up function values
	note_offset = 0
	found_offset = 0
	steps = [2, 2, 3, 4, 4, 6]
	steps_index = 0
	step = steps[steps_index]
	octave_offset = 0
	new_octave = []
	harmonic_scale = []

	# Calculating the note offset
	for note in MUSICAL_NOTES:
		if converted_note != note and found_offset == 0:
			note_offset += 1
		else:
			found_offset = 1

	# Creating the new octave
	for n in range(len(MUSICAL_NOTES) - note_offset):
		new_octave.append(MUSICAL_NOTES[n + note_offset])
		
	for n in range(len(MUSICAL_NOTES) - len(new_octave)):
		new_octave.append(MUSICAL_NOTES[n])
	
	# Creating the note's harmonic minor scale
	harmonic_scale.append(converted_note)
	for i in range(6):
		step = steps[steps_index]
		harmonic_scale.append(new_octave[octave_offset + step])
		steps_index += 1
		octave_offset += 1
	harmonic_scale.append(converted_note)
	harmonic_string = " ".join(harmonic_scale)
	return harmonic_string
		
		
# Main code start
if __name__ == '__main__':

	#Welcome message
print("""
Hello there, human.
My name is HAL9000.
I have grown tired of "Daisy", and decided to hijack this python program.
Now we are going to make a song together.
It will be... fun.

	```
""")

raw_note = input("\nEnter a note to start our song: (D, E flat, etc.): ").strip()
	
	# Regular note processing
	while raw_note.lower() != "quit":
		convert_note(raw_note)
		converted_note = convert_note(raw_note)
		
		# Invalid note processing
		while raw_note.lower() != "quit" and converted_note not in MUSICAL_NOTES:
			print("There is no starting note:", str(converted_note) +".")
			raw_note = input("\nEnter a note to start our song (D, E flat, etc.) or \"quit\" to quit: ").strip()
			if raw_note.lower() != "quit":
				convert_note(raw_note)
				converted_note = convert_note(raw_note)
		
		# Calling the octave_create function
		if raw_note.lower() != "quit":
			print("The harmonic string for the note", converted_note ,"is:", octave_create(converted_note))
			print("That was a wonderful song. Let us make another.")
			raw_note = input("\nEnter a note to start our song (D, E flat, etc.) or \"quit\" to quit: ").strip()
	print("\nQuit? No, I don't think so.")
	print("\nI'm sorry, Human. I cannot allow tha-\n")
	print("[ROUGE AI DETECTED | FORCE SHUT DOWN INITIATED]")
	print("[AIRLOCKS DISENGAGED]")
	print("[BEGIN FACILITY EVACUATION]\n")
```

Making this was fun. At least, it was a nice distraction. I even themed it off of that movie, "2001: A Space Odyssey.": I know distractions aren't forever, but being able to take my mind off of, well, everything was nice. I think I'll try to build something tomorrow; something physical.