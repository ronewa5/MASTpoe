# MASTpoe
poepart2
import React, { useState } from 'react';
import { View, Text, Button, StyleSheet, TouchableOpacity, Modal, FlatList, TextInput } from 'react-native';


const courses = [
  { name: 'Starters', price: 'R5', description: '' },
  { name: 'Mains', price: 'R15', description: '' },
  { name: 'Desert', price: 'R8', description: '' },
];

const CourseSelector: React.FC = () => {
  
  const [currentIndex, setCurrentIndex] = useState(0);
  const [isMenuVisible, setMenuVisible] = useState(false);
  const [descriptions, setDescriptions] = useState(courses.map(course => course.description));

  
  const handleCourseSelect = (index: number) => {
    setCurrentIndex(index);
    setMenuVisible(false);
  };

  
  const handleDescriptionChange = (text: string, index: number) => {
    const newDescriptions = [...descriptions];
    newDescriptions[index] = text;
    setDescriptions(newDescriptions);
  };

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Welcome Christoffel</Text>
      <Text style={styles.courseText}>Current Course: {courses[currentIndex].name}</Text>
      <Text style={styles.priceText}>Price: {courses[currentIndex].price}</Text>

  
      <TextInput
        style={styles.input}
        placeholder={`Enter description for ${courses[currentIndex].name}`}
        value={descriptions[currentIndex]}
        onChangeText={(text) => handleDescriptionChange(text, currentIndex)}
      />

      
      <TouchableOpacity style={styles.menuButton} onPress={() => setMenuVisible(true)}>
        <Text style={styles.menuButtonText}>Menu</Text>
      </TouchableOpacity>

      
      <Modal visible={isMenuVisible} transparent={true} animationType="slide">
        <View style={styles.modalContainer}>
          <View style={styles.modalContent}>
            <Text style={styles.modalTitle}>Choose a Course</Text>
            <FlatList
              data={courses}
              keyExtractor={(item) => item.name}
              renderItem={({ item, index }) => (
                <TouchableOpacity
                  style={styles.courseOption}
                  onPress={() => handleCourseSelect(index)}
                >
                  <Text style={styles.courseOptionText}>{item.name}</Text>
                  <Text style={styles.courseOptionPrice}>{item.price}</Text>
                </TouchableOpacity>
              )}
            />
            <Button title="Close" onPress={() => setMenuVisible(false)} />
          </View>
        </View>
      </Modal>
    </View>
  );
};

export default CourseSelector;


const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#ff20',
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold',
    marginBottom: 20,
  },
  courseText: {
    fontSize: 20,
    marginVertical: 10,
  },
  priceText: {
    fontSize: 18,
    marginBottom: 20,
    color: 'green',
  },
  input: {
    height: 40,
    borderColor: 'gray',
    borderWidth: 1,
    width: 250,
    marginBottom: 20,
    paddingLeft: 10,
  },
  menuButton: {
    backgroundColor: '#6200ea',
    padding: 10,
    borderRadius: 5,
    marginTop: 20,
  },
  menuButtonText: {
    color: '#ff2',
    fontSize: 16,
  },
  modalContainer: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: 'rgba(0, 5, 5, 5.10)',
  },
  modalContent: {
    width: '80%',
    backgroundColor: 'blue',
    padding: 20,
    borderRadius: 10,
    alignItems: 'center',
  },
  modalTitle: {
    fontSize: 20,
    marginBottom: 20,
  },
  courseOption: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    padding: 15,
    borderBottomWidth: 1,
    borderBottomColor: '#ff2',
    width: '100%',
  },
  courseOptionText: {
    fontSize: 18,
  },
  courseOptionPrice: {
    fontSize: 18,
    color: 'green',
  },
});
