# Smart Study Planner
# Individual Assignment
# This program allows students to record, view, search and analyse
# their study sessions. Data is saved to study_log.txt.

FILE_NAME = "study_log.txt"


def classify_session(duration):
    """
    Classifies a study session according to its duration.
    """
    if duration < 30:
        return "Short"
    elif duration <= 90:
        return "Medium"
    else:
        return "Long"


def add_session(sessions):
    """
    Prompts the user for study session details and adds
    the session to the sessions list.
    """

    print("\n--- Add Study Session ---")

    subject = input("Enter subject name: ").strip()
    topic = input("Enter topic covered: ").strip()
    date = input("Enter date/day label: ").strip()

    # Keep asking until the user enters a positive number.
    while True:
        try:
            duration = float(input("Enter duration in minutes: "))

            if duration > 0:
                break
            else:
                print("Duration must be a positive number.")

        except ValueError:
            print("Invalid input. Please enter a number.")

    session = {
        "subject": subject,
        "topic": topic,
        "date": date,
        "duration": duration
    }

    sessions.append(session)

    print("Study session added successfully!")


def view_sessions(sessions):
    """
    Displays all recorded study sessions in a formatted table.
    """

    print("\n--- All Study Sessions ---")

    if not sessions:
        print("No study sessions have been recorded.")
        return

    print("-" * 90)
    print(
        f"{'Subject':<20}"
        f"{'Topic':<25}"
        f"{'Date':<15}"
        f"{'Duration':<12}"
        f"{'Class':<10}"
    )
    print("-" * 90)

    for session in sessions:
        classification = classify_session(session["duration"])

        print(
            f"{session['subject']:<20}"
            f"{session['topic']:<25}"
            f"{session['date']:<15}"
            f"{session['duration']:<12.1f}"
            f"{classification:<10}"
        )

    print("-" * 90)


def search_by_subject(sessions, subject):
    """
    Searches for study sessions by subject.
    Matching is case-insensitive.
    """

    print(f"\n--- Search Results for: {subject} ---")

    matching_sessions = []

    for session in sessions:
        if session["subject"].lower() == subject.lower():
            matching_sessions.append(session)

    if not matching_sessions:
        print(f"No study sessions found for '{subject}'.")
        return

    print("-" * 90)
    print(
        f"{'Subject':<20}"
        f"{'Topic':<25}"
        f"{'Date':<15}"
        f"{'Duration':<12}"
        f"{'Class':<10}"
    )
    print("-" * 90)

    total_minutes = 0

    for session in matching_sessions:
        classification = classify_session(session["duration"])

        print(
            f"{session['subject']:<20}"
            f"{session['topic']:<25}"
            f"{session['date']:<15}"
            f"{session['duration']:<12.1f}"
            f"{classification:<10}"
        )

        total_minutes += session["duration"]

    print("-" * 90)
    print(f"Total time spent on {subject}: {total_minutes:.1f} minutes")
    print(f"Total time in hours: {total_minutes / 60:.2f} hours")


def study_statistics(sessions):
    """
    Calculates and displays study statistics.
    """

    print("\n--- Study Statistics ---")

    if not sessions:
        print("No study sessions available for statistics.")
        return

    # Calculate total study time.
    total_minutes = sum(session["duration"] for session in sessions)
    total_hours = total_minutes / 60

    print(f"Total hours studied overall: {total_hours:.2f} hours")

    # Calculate total study time for each subject.
    subject_totals = {}

    for session in sessions:
        subject = session["subject"]

        if subject not in subject_totals:
            subject_totals[subject] = 0

        subject_totals[subject] += session["duration"]

    print("\nTotal study time per subject:")

    for subject, minutes in subject_totals.items():
        print(f"- {subject}: {minutes / 60:.2f} hours")

    # Find the subject with the least amount of study time.
    weakest_subject = min(subject_totals, key=subject_totals.get)

    print(
        f"\nSubject with the least study time "
        f"(weakest area): {weakest_subject}"
    )
    print(
        f"Time spent on {weakest_subject}: "
        f"{subject_totals[weakest_subject] / 60:.2f} hours"
    )

    # Find the longest single study session.
    longest_session = max(sessions, key=lambda session: session["duration"])

    print("\nLongest single study session:")
    print(f"Subject: {longest_session['subject']}")
    print(f"Topic: {longest_session['topic']}")
    print(f"Date: {longest_session['date']}")
    print(f"Duration: {longest_session['duration']:.1f} minutes")
    print(
        f"Classification: "
        f"{classify_session(longest_session['duration'])}"
    )


def save_sessions(sessions):
    """
    Saves all study sessions to study_log.txt.
    """

    try:
        with open(FILE_NAME, "w") as file:

            for session in sessions:
                # Store each session using | as a separator.
                file.write(
                    f"{session['subject']}|"
                    f"{session['topic']}|"
                    f"{session['date']}|"
                    f"{session['duration']}\n"
                )

        print("Study sessions saved successfully.")

    except OSError as error:
        print(f"Error saving sessions: {error}")


def load_sessions():
    """
    Loads previously saved sessions from study_log.txt.
    If the file does not exist, an empty list is returned.
    """

    sessions = []

    try:
        with open(FILE_NAME, "r") as file:

            for line in file:
                line = line.strip()

                if not line:
                    continue

                parts = line.split("|")

                if len(parts) == 4:
                    subject = parts[0]
                    topic = parts[1]
                    date = parts[2]
                    duration = float(parts[3])

                    session = {
                        "subject": subject,
                        "topic": topic,
                        "date": date,
                        "duration": duration
                    }

                    sessions.append(session)

    except FileNotFoundError:
        # This is normal during the first run of the program.
        print("No existing study log found. Starting with an empty log.")

    except (ValueError, OSError) as error:
        print(f"Error loading study sessions: {error}")

    return sessions


def display_menu():
    """
    Displays the main menu.
    """

    print("\n" + "=" * 50)
    print("           SMART STUDY PLANNER")
    print("=" * 50)
    print("1. Add a study session")
    print("2. View all sessions")
    print("3. Search sessions by subject")
    print("4. View statistics")
    print("5. Save and exit")
    print("=" * 50)


def main():
    """
    Main function controlling the Smart Study Planner.
    """

    # Load previously saved sessions when the program starts.
    sessions = load_sessions()

    while True:

        display_menu()

        choice = input("Enter your choice (1-5): ").strip()

        if choice == "1":
            add_session(sessions)

        elif choice == "2":
            view_sessions(sessions)

        elif choice == "3":
            subject = input("Enter subject to search: ").strip()
            search_by_subject(sessions, subject)

        elif choice == "4":
            study_statistics(sessions)

        elif choice == "5":
            save_sessions(sessions)
            print("Thank you for using Smart Study Planner!")
            print("Program closed.")
            break

        else:
            print("Invalid choice. Please select an option from 1 to 5.")


# Program entry point
if __name__ == "__main__":
    main()
