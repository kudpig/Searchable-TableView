# Searchable-TableView
TableViewに表示されている文字を検索する

[![Image from Gyazo](https://i.gyazo.com/cb9c95372a6ce77b2edd9111e7fc5dd7.png)](https://gyazo.com/cb9c95372a6ce77b2edd9111e7fc5dd7)

### 参考
[Searchable Table View in Swift with Xcode 11 | iOS for Beginners](https://www.youtube.com/watch?v=-UQcifmThag&t=3s)

## ソースコード
## ViewController
```swift
import UIKit

class ViewController: UIViewController, UITableViewDelegate, UITableViewDataSource, UITextFieldDelegate {
    
    @IBOutlet var table: UITableView!
    @IBOutlet var field: UITextField!
    
    var data = [String]()
    var filteredData = [String]()
    var filtered = false

    override func viewDidLoad() {
        super.viewDidLoad()
        
        setUpData()
        
        table.delegate = self
        table.dataSource = self
        field.delegate = self
        
    }
    
    
    func textField(_ textField: UITextField, shouldChangeCharactersIn range: NSRange, replacementString string: String) -> Bool {
        
        if let text = textField.text {
            filteredText(text + string)
        }
        
        return true
    }
    
    func filteredText(_ query: String?) {
        
        guard let query = query else {
            return
        }
        
        filteredData.removeAll()
        for string in data {
            if string.lowercased().starts(with: query.lowercased()) {
                filteredData.append(string)
            }
        }
        table.reloadData()
        filtered = true
        
    }
    
    private func setUpData() {
        data.append("John")
        data.append("Abe")
        data.append("jenny")
        data.append("Dan")
        data.append("Zack")
        data.append("Luke")
        data.append("kevin")
        data.append("Briana")
        data.append("Melanie")
        data.append("Sarah")
        data.append("Shawn")
        data.append("Teri")
        data.append("Tom")
    }
    

    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        
        if !filteredData.isEmpty {
            return filteredData.count
        }
        
        return filtered ? 0 : data.count
    }
    
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = table.dequeueReusableCell(withIdentifier: "cell", for: indexPath)
        
        if !filteredData.isEmpty {
            cell.textLabel?.text = filteredData[indexPath.row]
        } else {
            cell.textLabel?.text = data[indexPath.row]
        }

        return cell
    }
    
    func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        
    }

}
```
