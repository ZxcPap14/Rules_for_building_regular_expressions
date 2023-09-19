# Rules_for_building_regular_expressions
Create by: Денис Казанцев & Артем Николаев
-Lib


    using Microsoft.SqlServer.Server;
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Text.RegularExpressions;
    using System.Threading.Tasks;
    
    namespace RegexLib1
    {
        public class CheckSymbols
        {
            /// <summary>
            /// В качестве параметра передается строка, которая может быть пустой или содержать произвольные символы.
            /// </summary>
            /// <param name="textString"></param>
            /// <returns>
            /// Метод возвращает true, если переданная строка соответствует email В противном случае возвращается false.
            /// </returns>
            public static bool IsEmail(string textString)
            {
                string regex = @"^[a-z]+\@[a-z]+\.[a-z]+$";

            if (string.IsNullOrEmpty(textString))
            {
                return false;
            }
            if (Regex.Match(textString, regex,RegexOptions.IgnoreCase).Success )
            {
              return true;
            }
            return false;
        }
        /// <summary>
        /// В качестве параметра передается строка, которая может быть пустой или содержать произвольные символы.
        /// </summary>
        /// <param name="textString"></param>
        /// <returns>
        /// Метод возвращает true, если переданная строка соответствует условиям выше и является корректным номером телефона. В противном случае возвращается false.
        /// </returns>
        public static bool IsPhoneNumber(string textString)
        {
            string regex = @"^((8|\+7)[\- ]?)(\(?\d{3}\)?[\- ]?)?[\d\- ]{7,10}$";
            if (string.IsNullOrEmpty(textString)) 
            { 
                return false; 
            }
            if (Regex.Match(textString, regex).Success)
            {
                return true;
            }
        ;

            return false;
        }
        public static bool Password(string textString)
        {
            string regex = @"(?=.+[!@#$&*])(?=.+[0-9])(?=.+[A-Z].+[a-z]).{8,15}";
            if (string.IsNullOrEmpty(textString))
            {
                return false;
            }
            if (Regex.Match(textString,regex).Success)
            {
                return true;
            }

            return false;
        }




    }
    }
-Tests


    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using System;
    using RegexLib1;
    
    namespace RegexLibTests
    {
        [TestClass]
        public class CheckSymbolsTests
        {
            /// <summary>
            /// CheckMail True/False
            /// </summary>
            [TestMethod]
            public void ChekMail_RightMail_ReturneTrue()
            {
                //Arrange
                string textstring = "Deniskaz@mail.ru";
                //Act
                bool result = CheckSymbols.IsEmail(textstring);
                //Assert
                Assert.IsTrue(result);

        }
        [TestMethod]
        public void ChekMail_WrongMail_ReturneTrue()
        {
            //Arrange
            string textstring = "Deniskazmail.ru";
            //Act
            bool result = CheckSymbols.IsEmail(textstring);
            //Assert
            Assert.IsFalse(result);

        }
        [TestMethod]
        public void ChekMail_Wrong2Mail_ReturneFalse()
        {
            //Arrange
            string textstring = "Deniskaz@mailru";
            //Act
            bool result = CheckSymbols.IsEmail(textstring);
            //Assert
            Assert.IsFalse(result);

        }
        [TestMethod]
        public void ChekMail_Wrong3Mail_ReturneFalse()
        {
            //Arrange
            string textstring = "Deniskaz@mail/ru";
            //Act
            bool result = CheckSymbols.IsEmail(textstring);
            //Assert
            Assert.IsFalse(result);

        }
        [TestMethod]
        public void ChekMail_Wrong4Mail_ReturneFalse()
        {
            //Arrange
            string textstring = "Deniskaz!mail.ru";
            //Act
            bool result = CheckSymbols.IsEmail(textstring);
            //Assert
            Assert.IsFalse(result);

        }
        [TestMethod]
        public void ChekPhone_RightNumber_ReturneFalse()
        {
            //Arrange
            string textstring = "+79555555555";
            //Act
            bool result = CheckSymbols.IsPhoneNumber(textstring);
            //Assert
            Assert.IsTrue(result);

        }
        [TestMethod]
        public void ChekPhone_WrongNumber_ReturneFalse()
        {
            //Arrange
            string textstring = "7abcde12345";
            //Act
            bool result = CheckSymbols.IsPhoneNumber(textstring);
            //Assert
            Assert.IsFalse(result);

        }
        [TestMethod]
        public void ChekPhone_WrongNumber2_ReturneFalse()
        {
            //Arrange
            string textstring = "+31234512345";
            //Act
            bool result = CheckSymbols.IsPhoneNumber(textstring);
            //Assert
            Assert.IsFalse(result);

        }
        [TestMethod]
        public void ChekPhone_WrongNumber3_ReturneFalse()
        {
            //Arrange
            string textstring = "+7123";
            //Act
            bool result = CheckSymbols.IsPhoneNumber(textstring);
            //Assert
            Assert.IsFalse(result);

        }
        public void CheckPassword_WrongPassword_ReturneFalse()
        {
            //Arrange
            string textstring = "111111111";
            //Act
            bool result = CheckSymbols.Password(textstring);
            //Assert
            Assert.IsFalse(result);
        }
        public void CheckPassword_WrongPassword2_ReturneFalse()
        {
            //Arrange
            string textstring = "aaaaaaaaaaaa";
            //Act
            bool result = CheckSymbols.Password(textstring);
            //Assert
            Assert.IsFalse(result);
        }
        public void CheckPassword_RightPassword_ReturneTrue()
        {
            //Arrange
            string textstring = "AEI3Ameva";
            //Act
            bool result = CheckSymbols.Password(textstring);
            //Assert
            Assert.IsTrue(result);
        }
        public void CheckPassword_RightPassword2_ReturnedTrue()
        {
            //Arrange
            string textstring = "y54whUc?#";
            //Act
            bool result = CheckSymbols.Password(textstring);
            //Assert
            Assert.IsTrue(result);
        }
    }
    }

