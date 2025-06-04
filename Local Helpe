import React, { useState, useEffect } from 'react';
import { 
  View, 
  Text, 
  StyleSheet, 
  Image, 
  TouchableOpacity, 
  ScrollView, 
  Platform,
  TextInput
} from 'react-native';
import { useNavigation, useRoute, RouteProp } from '@react-navigation/native';
import { SafeAreaView } from 'react-native-safe-area-context';
import { FontAwesome5, Ionicons, MaterialIcons, AntDesign } from '@expo/vector-icons';
import { toast } from "sonner-native";
import { RootStackParamList } from '../App';

// Define the param list types
type RootStackParamList = {
  ServiceProvider: {
    id: string;
    name: string;
    service: string;
    rating: number;
    reviews: number;
    verified: boolean;
    distance: string;
    imageUrl: string;
    emergencyAvailable: boolean;
    isEmergency: boolean;
  };
};

// Define the route prop type
type ServiceProviderScreenRouteProp = RouteProp<RootStackParamList, 'ServiceProvider'>;

// Define review type
type Review = {
  id: string;
  userName: string;
  rating: number;
  date: string;
  comment: string;
  userImage: string;
};

export default function ServiceProviderScreen() {
  const navigation = useNavigation();
  const route = useRoute<ServiceProviderScreenRouteProp>();
  const provider = route.params;
  
  const [selectedDate, setSelectedDate] = useState<string | null>(null);
  const [selectedTimeSlot, setSelectedTimeSlot] = useState<string | null>(null);
  const [isEmergency, setIsEmergency] = useState<boolean>(
    'isEmergency' in route.params ? Boolean(route.params.isEmergency) : false
  );

  // Auto-trigger emergency call if coming from emergency button
  useEffect(() => {
    if (isEmergency) {
      handleEmergencyCall();
      setIsEmergency(false); // Reset after handled
    }
  }, []);

  // Sample dates for booking
  const availableDates = [
    'Today',
    'Tomorrow',
    'Jun 5',
    'Jun 6',
    'Jun 7',
    'Jun 8',
  ];

  // Sample time slots
  const timeSlots = [
    '9:00 AM',
    '10:00 AM',
    '11:00 AM',
    '12:00 PM',
    '2:00 PM',
    '3:00 PM',
    '4:00 PM',
    '5:00 PM',
  ];

  // Sample reviews
  const reviews: Review[] = [
    {
      id: '1',
      userName: 'Amit Verma',
      rating: 5,
      date: '2 days ago',
      comment: 'Excellent service! Fixed my plumbing issue very quickly and professionally.',
      userImage: 'https://api.a0.dev/assets/image?text=AV&aspect=1:1',
    },
    {
      id: '2',
      userName: 'Neha Singh',
      rating: 4,
      date: '1 week ago',
      comment: 'Good work but arrived a bit late. Otherwise satisfied with the service.',
      userImage: 'https://api.a0.dev/assets/image?text=NS&aspect=1:1',
    },
    {
      id: '3',
      userName: 'Raj Kumar',
      rating: 5,
      date: '2 weeks ago',
      comment: 'Very courteous and skilled. Will definitely call again for future work.',
      userImage: 'https://api.a0.dev/assets/image?text=RK&aspect=1:1',
    },
  ];

  // Function to handle booking
  const handleBooking = () => {
    if (!selectedDate || !selectedTimeSlot) {
      toast.error('Please select both date and time slot');
      return;
    }
    
    toast.success(`Booking confirmed with ${provider.name} for ${selectedDate} at ${selectedTimeSlot}!`);
    // Here you would navigate to a confirmation screen or back to home
    navigation.goBack();
  };

  // Function to handle emergency call
  const handleEmergencyCall = () => {
    toast.success(`Connecting you with ${provider.name} for emergency service...`);
    // Here you would typically implement call functionality
  };

  // Render stars for ratings
  const renderStars = (rating: number) => {
    const stars = [];
    for (let i = 1; i <= 5; i++) {
      stars.push(
        <FontAwesome5 
          key={i} 
          name="star" 
          size={14} 
          solid={i <= rating} 
          color={i <= rating ? "#FFD700" : "#D3D3D3"} 
          style={{ marginRight: 2 }}
        />
      );
    }
    return stars;
  };

  return (
    <SafeAreaView style={styles.container}>
      <ScrollView showsVerticalScrollIndicator={Platform.OS === 'web'}>
        {/* Header with back button */}
        <View style={styles.header}>
          <TouchableOpacity 
            style={styles.backButton} 
            onPress={() => navigation.goBack()}
          >
            <Ionicons name="arrow-back" size={24} color="#333" />
          </TouchableOpacity>
          <Text style={styles.headerTitle}>Service Provider</Text>
          <TouchableOpacity style={styles.shareButton}>
            <Ionicons name="share-outline" size={24} color="#333" />
          </TouchableOpacity>
        </View>
        
        {/* Provider Info Card */}
        <View style={styles.profileCard}>
          <Image source={{ uri: provider.imageUrl }} style={styles.profileImage} />
          <View style={styles.profileInfo}>
            <View style={styles.nameRow}>
              <Text style={styles.profileName}>{provider.name}</Text>
              {provider.verified && (
                <View style={styles.verifiedBadge}>
                  <MaterialIcons name="verified" size={16} color="#1a73e8" />
                  <Text style={styles.verifiedText}>Verified</Text>
                </View>
              )}
            </View>
            <Text style={styles.serviceType}>{provider.service}</Text>
            <View style={styles.ratingRow}>
              <View style={styles.starsContainer}>
                {renderStars(provider.rating)}
              </View>
              <Text style={styles.ratingText}>
                {provider.rating} ({provider.reviews} reviews)
              </Text>
            </View>
            <View style={styles.locationRow}>
              <Ionicons name="location-outline" size={16} color="#666" />
              <Text style={styles.locationText}>{provider.distance} away</Text>
            </View>
          </View>
        </View>
        
        {/* Quick Actions */}
        <View style={styles.quickActions}>
          <TouchableOpacity style={styles.actionButton}>
            <Ionicons name="call-outline" size={20} color="#1a73e8" />
            <Text style={styles.actionText}>Call</Text>
          </TouchableOpacity>
          <TouchableOpacity style={styles.actionButton}>
            <Ionicons name="chatbubble-outline" size={20} color="#1a73e8" />
            <Text style={styles.actionText}>Chat</Text>
          </TouchableOpacity>
          <TouchableOpacity style={styles.actionButton}>
            <Ionicons name="heart-outline" size={20} color="#1a73e8" />
            <Text style={styles.actionText}>Save</Text>
          </TouchableOpacity>
        </View>
        
        {/* About Section */}
        <View style={styles.section}>
          <Text style={styles.sectionTitle}>About</Text>
          <Text style={styles.aboutText}>
            Experienced {provider.service.toLowerCase()} with over 5 years of professional work. 
            Specializes in residential and commercial services with quick response time 
            and quality workmanship.
          </Text>
        </View>
        
        {/* Services Section */}
        <View style={styles.section}>
          <Text style={styles.sectionTitle}>Services Offered</Text>
          <View style={styles.servicesList}>
            <View style={styles.serviceItem}>
              <FontAwesome5 name="check-circle" size={16} color="#1a73e8" solid />
              <Text style={styles.serviceItemText}>Installation</Text>
            </View>
            <View style={styles.serviceItem}>
              <FontAwesome5 name="check-circle" size={16} color="#1a73e8" solid />
              <Text style={styles.serviceItemText}>Repair</Text>
            </View>
            <View style={styles.serviceItem}>
              <FontAwesome5 name="check-circle" size={16} color="#1a73e8" solid />
              <Text style={styles.serviceItemText}>Maintenance</Text>
            </View>
            <View style={styles.serviceItem}>
              <FontAwesome5 name="check-circle" size={16} color="#1a73e8" solid />
              <Text style={styles.serviceItemText}>Consultation</Text>
            </View>
          </View>
        </View>
        
        {/* Book a Service Section */}
        <View style={styles.section}>
          <Text style={styles.sectionTitle}>Book a Service</Text>
          
          {/* Date Selection */}
          <Text style={styles.subTitle}>Select Date</Text>
          <ScrollView horizontal showsHorizontalScrollIndicator={false} style={styles.dateContainer}>
            {availableDates.map((date, index) => (
              <TouchableOpacity
                key={index}
                style={[
                  styles.dateOption,
                  selectedDate === date ? styles.selectedDateOption : {}
                ]}
                onPress={() => setSelectedDate(date)}
              >
                <Text 
                  style={[
                    styles.dateText,
                    selectedDate === date ? styles.selectedDateText : {}
                  ]}
                >
                  {date}
                </Text>
              </TouchableOpacity>
            ))}
          </ScrollView>
          
          {/* Time Slot Selection */}
          <Text style={styles.subTitle}>Select Time Slot</Text>
          <View style={styles.timeSlotContainer}>
            {timeSlots.map((time, index) => (
              <TouchableOpacity
                key={index}
                style={[
                  styles.timeSlot,
                  selectedTimeSlot === time ? styles.selectedTimeSlot : {}
                ]}
                onPress={() => setSelectedTimeSlot(time)}
              >
                <Text 
                  style={[
                    styles.timeSlotText,
                    selectedTimeSlot === time ? styles.selectedTimeSlotText : {}
                  ]}
                >
                  {time}
                </Text>
              </TouchableOpacity>
            ))}
          </View>
          
          {/* Special Instructions */}
          <Text style={styles.subTitle}>Special Instructions (Optional)</Text>
          <TextInput
            style={styles.instructionsInput}
            placeholder="Add any special requirements here..."
            multiline={true}
            numberOfLines={3}
          />
        </View>
        
        {/* Reviews Section */}
        <View style={styles.section}>
          <View style={styles.reviewsHeader}>
            <Text style={styles.sectionTitle}>Reviews</Text>
            <TouchableOpacity style={styles.seeAllButton}>
              <Text style={styles.seeAllText}>See All</Text>
            </TouchableOpacity>
          </View>
          
          {reviews.map((review) => (
            <View key={review.id} style={styles.reviewCard}>
              <View style={styles.reviewerInfo}>
                <Image source={{ uri: review.userImage }} style={styles.reviewerImage} />
                <View>
                  <Text style={styles.reviewerName}>{review.userName}</Text>
                  <View style={styles.reviewRating}>
                    {renderStars(review.rating)}
                    <Text style={styles.reviewDate}>{review.date}</Text>
                  </View>
                </View>
              </View>
              <Text style={styles.reviewComment}>{review.comment}</Text>
            </View>
          ))}
        </View>
      </ScrollView>
      
      {/* Bottom Action Bar */}
      <View style={styles.bottomBar}>
        {provider.emergencyAvailable && (
          <TouchableOpacity 
            style={styles.emergencyButton}
            onPress={handleEmergencyCall}
          >
            <MaterialIcons name="call" size={20} color="#ffffff" />
            <Text style={styles.emergencyText}>Emergency</Text>
          </TouchableOpacity>
        )}
        <TouchableOpacity 
          style={[
            styles.bookButton,
            (!selectedDate || !selectedTimeSlot) ? styles.disabledButton : {}
          ]}
          onPress={handleBooking}
          disabled={!selectedDate || !selectedTimeSlot}
        >
          <Text style={styles.bookButtonText}>Book Now</Text>
        </TouchableOpacity>
      </View>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#f8f9fa',
  },
  header: {
    flexDirection: 'row',
    alignItems: 'center',
    justifyContent: 'space-between',
    padding: 16,
  },
  backButton: {
    padding: 8,
  },
  headerTitle: {
    fontSize: 18,
    fontWeight: 'bold',
    color: '#333',
  },
  shareButton: {
    padding: 8,
  },
  profileCard: {
    flexDirection: 'row',
    backgroundColor: 'white',
    borderRadius: 12,
    marginHorizontal: 16,
    padding: 16,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    shadowRadius: 4,
    elevation: 2,
  },
  profileImage: {
    width: 80,
    height: 80,
    borderRadius: 40,
  },
  profileInfo: {
    marginLeft: 16,
    flex: 1,
  },
  nameRow: {
    flexDirection: 'row',
    alignItems: 'center',
  },
  profileName: {
    fontSize: 18,
    fontWeight: 'bold',
    marginRight: 8,
    color: '#333',
  },
  verifiedBadge: {
    flexDirection: 'row',
    alignItems: 'center',
    backgroundColor: '#e8f1ff',
    paddingHorizontal: 6,
    paddingVertical: 2,
    borderRadius: 4,
  },
  verifiedText: {
    fontSize: 10,
    color: '#1a73e8',
    marginLeft: 2,
  },
  serviceType: {
    color: '#666',
    fontSize: 14,
    marginTop: 2,
  },
  ratingRow: {
    flexDirection: 'row',
    alignItems: 'center',
    marginTop: 4,
  },
  starsContainer: {
    flexDirection: 'row',
    marginRight: 6,
  },
  ratingText: {
    color: '#666',
    fontSize: 12,
  },
  locationRow: {
    flexDirection: 'row',
    alignItems: 'center',
    marginTop: 4,
  },
  locationText: {
    color: '#666',
    fontSize: 12,
    marginLeft: 4,
  },
  quickActions: {
    flexDirection: 'row',
    justifyContent: 'space-around',
    backgroundColor: 'white',
    borderRadius: 12,
    marginHorizontal: 16,
    marginTop: 16,
    padding: 12,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 1 },
    shadowOpacity: 0.05,
    shadowRadius: 2,
    elevation: 1,
  },
  actionButton: {
    alignItems: 'center',
    padding: 8,
  },
  actionText: {
    color: '#1a73e8',
    fontSize: 12,
    marginTop: 4,
  },
  section: {
    backgroundColor: 'white',
    borderRadius: 12,
    marginHorizontal: 16,
    marginTop: 16,
    padding: 16,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 1 },
    shadowOpacity: 0.05,
    shadowRadius: 2,
    elevation: 1,
  },
  sectionTitle: {
    fontSize: 18,
    fontWeight: 'bold',
    color: '#333',
    marginBottom: 8,
  },
  aboutText: {
    color: '#666',
    lineHeight: 20,
    fontSize: 14,
  },
  servicesList: {
    marginTop: 8,
  },
  serviceItem: {
    flexDirection: 'row',
    alignItems: 'center',
    marginBottom: 8,
  },
  serviceItemText: {
    marginLeft: 8,
    color: '#444',
    fontSize: 14,
  },
  subTitle: {
    fontSize: 16,
    fontWeight: '600',
    color: '#444',
    marginTop: 16,
    marginBottom: 8,
  },
  dateContainer: {
    flexDirection: 'row',
    marginBottom: 8,
  },
  dateOption: {
    backgroundColor: '#f0f4fc',
    paddingHorizontal: 16,
    paddingVertical: 10,
    borderRadius: 8,
    marginRight: 8,
  },
  selectedDateOption: {
    backgroundColor: '#1a73e8',
  },
  dateText: {
    color: '#444',
    fontWeight: '500',
  },
  selectedDateText: {
    color: 'white',
  },
  timeSlotContainer: {
    flexDirection: 'row',
    flexWrap: 'wrap',
    marginBottom: 8,
  },
  timeSlot: {
    backgroundColor: '#f0f4fc',
    paddingHorizontal: 16,
    paddingVertical: 10,
    borderRadius: 8,
    marginRight: 8,
    marginBottom: 8,
  },
  selectedTimeSlot: {
    backgroundColor: '#1a73e8',
  },
  timeSlotText: {
    color: '#444',
    fontWeight: '500',
  },
  selectedTimeSlotText: {
    color: 'white',
  },
  instructionsInput: {
    backgroundColor: '#f0f4fc',
    borderRadius: 8,
    padding: 12,
    height: 80,
    textAlignVertical: 'top',
    fontSize: 14,
    color: '#333',
  },
  reviewsHeader: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    alignItems: 'center',
  },
  seeAllButton: {
    padding: 4,
  },
  seeAllText: {
    color: '#1a73e8',
    fontSize: 14,
  },
  reviewCard: {
    marginTop: 12,
    paddingTop: 12,
    borderTopWidth: 1,
    borderTopColor: '#f0f0f0',
  },
  reviewerInfo: {
    flexDirection: 'row',
    alignItems: 'center',
  },
  reviewerImage: {
    width: 40,
    height: 40,
    borderRadius: 20,
    marginRight: 12,
  },
  reviewerName: {
    fontWeight: '600',
    fontSize: 14,
    color: '#333',
  },
  reviewRating: {
    flexDirection: 'row',
    alignItems: 'center',
    marginTop: 2,
  },
  reviewDate: {
    fontSize: 12,
    color: '#888',
    marginLeft: 4,
  },
  reviewComment: {
    marginTop: 8,
    fontSize: 14,
    lineHeight: 20,
    color: '#555',
  },
  bottomBar: {
    backgroundColor: 'white',
    flexDirection: 'row',
    paddingHorizontal: 16,
    paddingVertical: 12,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: -2 },
    shadowOpacity: 0.1,
    shadowRadius: 4,
    elevation: 5,
  },
  emergencyButton: {
    flexDirection: 'row',
    backgroundColor: '#ff4757',
    paddingVertical: 12,
    paddingHorizontal: 16,
    borderRadius: 8,
    alignItems: 'center',
    justifyContent: 'center',
    marginRight: 12,
    flex: 1,
  },
  emergencyText: {
    color: '#fff',
    fontWeight: 'bold',
    fontSize: 14,
    marginLeft: 8,
  },
  bookButton: {
    backgroundColor: '#1a73e8',
    paddingVertical: 12,
    borderRadius: 8,
    alignItems: 'center',
    flex: 2,
  },
  disabledButton: {
    backgroundColor: '#a0c2f2',
  },
  bookButtonText: {
    color: '#fff',
    fontWeight: 'bold',
    fontSize: 16,
  },
});
