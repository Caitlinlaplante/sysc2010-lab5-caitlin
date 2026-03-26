import math
import unittest
from Lab5_Classes import Numbers
from Lab5_Classes import ECG

#4
class TestNumbers(unittest.TestCase):
    def setUp(self):
        self.number = Numbers(10)
    #4.1
    def test_factorial(self):
        self.assertEqual(self.number.factorial(4), 24, 'The factorial is right.')
        self.assertNotEqual(self.number.factorial(6), 700, 'The factorial is wrong.')
        self.assertEqual(self.number.factorial(1), 1, 'Negative not allowed.')

    #4.2
    def test_addToSum(self):
        self.number.addToSum(5)
        self.assertEqual(self.number.sum, 15, "Sum should increase by 5")
    
    def testmultiple_addToSum(self):
        self.number.addToSum(3)
        self.number.addToSum(2)
        self.assertEqual(self.number.sum, 15, "Sum should accumulate add 5")

    def test_subtractFromSm(self):
        self.number.subtractFromSum(4)
        self.assertEqual(self.number.sum, 6, "Sum should decrease by 4")
    
    def testmultiple_subtractFromSum(self):
        self.number.subtractFromSum(3)
        self.number.subtractFromSum(2)
        self.assertEqual(self.number.sum, 5, "Sum should accumulate subtract 5")
    
    def test_add_and_subtract(self):
        self.number.addToSum(5)
        self.number.subtractFromSum(3)
        self.assertEqual(self.number.sum, 12, "Combined operations should work")

    #4.3
    def test_stringOfNumber(self):
        self.assertEqual(self.number.stringOfNumber(5), "five", "the string is 5")
        self.assertNotEqual(self.number.stringOfNumber(5), "four", "the string is 5")

#5
class TestECG(unittest.TestCase):
    def setUp(self):
        self.test_signal = [0.1, 0.2, 1.2, 0.3, 0.1, 1.5, 0.2]
        self.ecg = ECG()
    #5.1
    def test_detect_peaks(self):
        peaks = self.ecg.detect_peaks(self.test_signal, 0.5)
        self.assertEqual(peaks, [2,5],"Should detect peaks at 2 and 5")

    def test_detect_no_peaks(self):
        signal = [0.1, 0.2, 0.3, 0.4]
        peaks = self.ecg.detect_peaks(signal, 0.1)
        self.assertEqual(peaks, [], "Should detect no peaks")

    #5.2
    def test_remove_baseline(self):
        result = self.ecg.remove_baseline(self.test_signal)
        expected = [-0.41428571428571437,-0.31428571428571433,0.6857142857142856,-0.21428571428571436,-0.41428571428571437,0.9857142857142857,-0.31428571428571433]
        self.assertEqual(result, expected)

    #5.3
    def test_normalize(self):
        result = self.ecg.normalize(self.test_signal)
        expected = [0.06666666666666667,0.13333333333333333,0.7999999999999999,0.19999999999999998,0.06666666666666667,1.0,0.13333333333333333]
        self.assertEqual(result, expected)

    #6
    #6.1
    def test_count_peaks(self):
        #No peaks
        signal_no_peak = [0.1,0.2,0.1,0.2]
        self.assertEqual(self.ecg.count_peaks(signal_no_peak, 0.5), 0)
        #One peak
        signal_one_peak = [0.1,0.6,0.1]
        self.assertEqual(self.ecg.count_peaks(signal_one_peak,0.5),1)
        #More than one peak
        self.assertEqual(self.ecg.count_peaks(self.test_signal,0.5),2)
        #Below threshold
        signal_below = [0.1, 0.4, 0.1, 0.3, 0.1]
        self.assertEqual(self.ecg.count_peaks(signal_below,0.5),0)
    
    #6.2
    def test_rr_intervals(self):
        #Empty peaks
        self.assertEqual(self.ecg.rr_intervals([],2),[])

        #Single peak
        self.assertEqual(self.ecg.rr_intervals([5],2),[])

        #More than one peak
        peaks = self.ecg.detect_peaks(self.test_signal, 0.5)
        self.assertEqual(self.ecg.rr_intervals(peaks,2),[1.5])

    #6.3
    def test_is_signal_valid(self):
        #Non numeric values
        self.assertFalse(self.ecg.is_signal_valid([0.1, "a", 0.3]))
        self.assertFalse(self.ecg.is_signal_valid([0.1, None, 0.2]))
        self.assertFalse(self.ecg.is_signal_valid([0.1, [1], 0.2]))
        #Integer
        self.assertTrue(self.ecg.is_signal_valid([1,2,3,4]))
        #Floats
        self.assertTrue(self.ecg.is_signal_valid(self.test_signal))
        #Mix of Float and Intergers
        self.assertTrue(self.ecg.is_signal_valid([0.1, 4, 0.3]))

    #7
    def test_heart_rate(self):
        #Invalid signal
        with self.assertRaises(ValueError):
            self.ecg.heart_rate([6,"hello",5,7],2)

        #Less than 2 peaks
        with self.assertRaises(ValueError):
            self.ecg.heart_rate([1],2)

        #With at least 2 peaks
        self.assertEqual(self.ecg.heart_rate([2,5],2),40.0)

if __name__ == '__main__':
    unittest.main()