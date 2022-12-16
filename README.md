# Calendor_WithoutPod
There Is a CalendorView File in this project ,so Only drag and Drop this File and Write below Code on a Controller Where you have to Show Calendor
Copy and Paste these Code onto the Controller


import UIKit
class CalendorViewController: UIViewController {
    var calenderView: CalendarView!
    var dateLabel: UILabel!
    var selectedDateLabel: UILabel!

    override func viewDidLoad() {
        super.viewDidLoad()
        calenderView = CalendarView()
        calenderView.didSelectDate = { [weak self] selectedDate in
            guard let self = self else { return }
            self.dateLabel.text = selectedDate?.date.shortDateFormat
        }
        setupLabel()
        setupConstraints()
    }
    
    private func setupLabel() {
        selectedDateLabel = UILabel()
        selectedDateLabel.font = .preferredFont(forTextStyle: .headline)
        selectedDateLabel.text = "Selected Date"
        selectedDateLabel.textAlignment = .center
        
        dateLabel = UILabel()
        dateLabel.font = .preferredFont(forTextStyle: .title1)
        dateLabel.text = Date().shortDateFormat
        dateLabel.textAlignment = .center
    }
    
    private func setupConstraints() {
        let mainStack = UIStackView(arrangedSubviews: [selectedDateLabel, dateLabel, calenderView])
        mainStack.axis = .vertical
        mainStack.translatesAutoresizingMaskIntoConstraints = false
        mainStack.spacing = 16
        mainStack.setCustomSpacing(8, after: selectedDateLabel)
        view.addSubview(mainStack)
        
        NSLayoutConstraint.activate([
            mainStack.leadingAnchor.constraint(equalTo: view.leadingAnchor),
            mainStack.trailingAnchor.constraint(equalTo: view.trailingAnchor),
            mainStack.centerYAnchor.constraint(equalTo: view.centerYAnchor),
            
            calenderView.heightAnchor.constraint(equalToConstant: view.bounds.height / 2),
        ])
    }
}

